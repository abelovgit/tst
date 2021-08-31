# idcons rulezzzz

<style>
mark{
    color:red;
}
</style>

<mark>what is DataBase</mark>

<!-- Tab links -->
<div class="tab">
  <button class="tablinks" onclick="openCity(event, 'tab1')">tab1</button>
  <button class="tablinks" onclick="openCity(event, 'tab2')">tab2</button>
</div>

<!-- Tab content -->
<div id="tab1" class="tabcontent">

# Table of contents
* [Environments](#environments)
* [Databases](#databases)
* [Running locally](#running-locally)
  * [Maven](#maven)
  * [Using Vagrant](#using-vagrant)
  * [IDEA](#idea)
  * [Command Line](#command-line)
  * [Setup Initial Data](#setup-initial-data)
  * [Docker](#docker)
  * [Mail service](#mail-service)
* [Debug](#debug)
* [Hotfixes](#hotfixes) 
  * [How do I make a change to what is in production?](#how-do-i-make-a-change-to-what-is-in-production)
  * [How do I take something which is already fixed on master (or another source branch) to production without taking along other commits already on master?](#how-do-i-take-something-which-is-already-fixed-on-master-or-another-source-branch-to-production-without-taking-along-other-commits-already-on-master)
* [How to replay events](#how-to-replay-events)
* [How to generate ETPA orders in ACC environment](#how-to-generate-etpa-orders-in-acc-environment)
* [How to apply a quick fix in the NGINX config](#how-to-apply-a-quick-fix-in-the-nginx-config)
* [How to copy data from ACC or PROD to your local laptop](#how-to-copy-data-from-acc-or-prod-to-your-local-laptop)
* [How to connect to mongodb acc/prod read/write](#how-to-connect-to-mongodb-accprod-readwrite)
* [How to connect to mongodb dev read/write](#how-to-connect-to-mongodb-dev-readwrite)
* [How to connect to mongodb acc/prod read/write (2)](#how-to-connect-to-mongodb-accprod-readwrite-2)
* [How to replace self signed certificates (For Mongodb nodes connection, WebApp to Mongodb connection & Manual operations connections)](#how-to-replace-self-signed-certificates-for-mongodb-nodes-connection-webapp-to-mongodb-connection--manual-operations-connections)
* [How to replace client facing certificates from external certificate authority](#how-to-replace-client-facing-certificates-from-external-certificate-authority)
* [How to replace Axon snapshot files](#how-to-replace-axon-snapshot-files)
* [How to update OR-tools](#how-to-update-or-tools)
* [How to analyse event handling performance](#how-to-analyse-event-handling-performance)
	
</div>

<div id="tab2" class="tabcontent">

### Environments
| Environment | Branches        | Links                                                                                                                               |
|-------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Test        | any (manual)    | [APP](https://tst.idcons.nl),[LOGS](https://tst.idcons.nl:5601),[METRICS](https://tst.idcons.nl:3000/)                              |
| Acceptance  | master (manual) | [APP](https://acc.idcons.nl),[LOGS](https://acc-monitoring.idcons.nl:5601),[METRICS](https://acc-monitoring.idcons.nl:3000/)        |
| Production  | master (manual) | [APP](https://idcons.nl),[LOGS](https://monitoring.idcons.nl:5601),[METRICS](https://monitoring.idcons.nl:3000/)                    |
 
NOTES: 
* Credentials can be found on https://pwsafe.trifork.nl
* OTP can be generated at https://totp.danhersam.com/

### DATABASES
| Environment | SSH Tunnel                                                                       | Links                                                                |
|-------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------|
| Test        | `ssh -L 8443:localhost:8443 -L 8081:localhost:8081 sysadmin@tst.idcons.nl`       | [MONGODB](https://localhost:8081/),[AXONDB](https://localhost:8443/) |
| Acceptance  | `ssh -L 8443:localhost:8443 -L 8081:localhost:8081 sysadmin@acc-db01.idcons.nl`  | [MONGODB](https://localhost:8081/),[AXONDB](https://localhost:8443/) |  
| Production  | `ssh -L 8443:localhost:8443 -L 8081:localhost:8081 sysadmin@db01.idcons.nl`      | [MONGODB](https://localhost:8081/),[AXONDB](https://localhost:8443/) |

For Mongo Acceptance, set up the tunnel, go to the link and use user 'idcons_ro' 

NOTES: 
* Credentials can be found on https://pwsafe.trifork.nl
* Establish the SSH tunnel before attempting to visit the prescribed ports on localhost

:fish: [Previous](#environments) | [To contents](#table-of-contents)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Running locally

##### Maven
Before building with Maven you need to add the missing dependency to the local repository:
```
./lib/install.sh
```

##### Using Vagrant
You can mimic cluster setup for mongo etc locally by using vagrant and virtualbox, Steps needed are:
* Download Vagrant and Virtualbox for your OS
* Run `deployment/vagrant/recreate.sh` 
* If not yet the case, add `Include config.d/*` as the FIRST line of ~/.ssh/config
* Use Ansible to populate the VMs using `deployment/ansible/run.sh vagrant`
* Run `vagrant status` inside the `vagrant` folder to retrieve hostnames, then connect to one of the instances using for example: `ssh idcons-db1`

To use existing VMs instead of recreating altogether (much faster after the first time), use `vagrant up` or just keep them running

##### IDEA
Add VM options in intellij run config:
```
-Djava.library.path=./lib/native
```
Add the following to the active profiles intellij run config:
```
dev
```

##### Command Line
```
./build.sh && ./run
```


##### Setup Initial Data
Some non prod test data:
```
curl -XPOST http://localhost:8080/setup
```

Initial prod data: 
```
curl -XPOST http://localhost:8080/setupproduction
```

##### Docker
For one time only to pull AxonDB image from private registry login with below command.
```bash
docker login gitlab.etpa.nl:4567
In case you get a message like this:
 Error response from daemon: Get https://gitlab.etpa.nl:4567/v2/: unauthorized: HTTP Basic: Access denied\nYou must use a personal access token with ‘api’ scope for Git over HTTP.\nYou can generate one at https://gitlab.etpa.nl/profile/personal_access_tokens
Then go to https://gitlab.etpa.nl/profile/personal_access_tokens and generate a token with 'api' scope. Next,
Try with:
docker login gitlab.etpa.nl:4567 -u <yourusername> -p <the generated token>
```
Get into docker directory in project and execute run script with 'wo' argument. 'wo' argument implies 'without application'. 
```bash
cd docker
./run.sh wo
```
If you want to run application and all databases containerized, get into docker directory in project and execute run script with 'w' argument. 'w' argument implies 'with application'.
```bash
cd docker
./run.sh w
```

Docker basics:
Look for all images, including the stopped images:
docker ps -a
Tail the logs on an image:
docker logs --follow <imageID>

Log onto docker instance: (exec for a command send to the image, ’ti’ for terminal, interactive, and ‘bash’ for the shell of course 
docker exec -ti docker_axondb_1 bash

##### Mail service
When using docker/run.sh for local development mailcatcher is available at http://localhost:1080.
Otherwise you can use 'fakesmtp' to catch outgoing emails when running in 'dev' mode. Just download and run it on its default port. Don't forget to start it....(common hickup)
java -jar fakeSMTP-2.0.jar will do, again....don't forget to start it....(common hickup)

[Previous](#databases) | [To contents](#table-of-contents)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Debug
Use the konami code to activate UI debugging: up, up, down, down, left, right, left, right, b, a
https://en.wikipedia.org/wiki/Konami_Code

[To contents](#table-of-contents)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Hotfixes 

NB: This is for emergencies only and should never become a frequent activity.

[To contents](#table-of-contents)

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------

##### How do I make a change to what is in production?

1. Check out the commit which is currently in prd: <br/>```git checkout <current_version_in_prd>```<br/>
2. Make a branch of it starting with "HOTFIX-": <br/>```git checkout -b HOTFIX-<name>```<br/>
3. Make, commit and push your changes:<br/>
```<make changes>```<br/>
```git add -A```<br/>
```git commit```<br/>
```git push```<br/>
4. Run the gitlab pipeline jobs the same way you would for the master branch.



##### How do I take something which is already fixed on master (or another source branch) to production without taking along other commits already on master?

1. Check out the commit which is currently in prd: <br/>```git checkout <current_version_in_prd>```<br/>
2. Make a branch of it: <br/>```git checkout -b HOTFIX-<name>```<br/>
3. Go to your source branch (let's assume master from here on out): <br/>```git checkout master```<br/>
4. Interactively rebase onto the version currently in prd: <br/>```git rebase -i HOTFIX-<name>```<br/>
5. Now delete all but the changes you want to take to prod (or pick something like "skip" if you're doing it in an IDE).
6. Complete the rebase. You now have a diverged version of master which can not be pushed, but can be used to merge locally.
7. Go back to your hotfix branch:<br/> 
`git checkout HOTFIX-<name>`
8. Merge in your special version of master <br/>```git merge master```<br/> (note that it's NOT origin/master, just master)<br/>
9. Push your hotfix branch: <br/>```git push```<br/>
10. Go back and fix your diverged master: <br/>```git checkout master```<br/> and <br/>```git reset --hard origin/master```<br/>

Your master branch is now back to normal and your hotfix branch contains only what's in prod plus the changes you hand picked during the rebase.

[comment]: <> (### How to replay events)

[comment]: <> (Run docker/replay.sh or execute manually:)

[comment]: <> (Get the appropriate token from the secrets in gitlab. The key is `idcons.replayToken`.)

[comment]: <> (Stop nginx by ssh'ing into the application server and stopping the nginx docker.)

[comment]: <> (Run the curl command:)

[comment]: <> (```)

[comment]: <> (curl -XPOST -H "Content-Type: application/json"  http://localhost:8080/eventprocessing/replayall -d "<token>")

[comment]: <> (```)

[comment]: <> (Start up the nginx docker container again.)


### How to generate ETPA orders in ACC environment
Use these urls to generate some orders in the ETPA ACC environment if you want to test the clearing of idcons:
https://nas.nijholt-energy.nl:9393/IDCONS/IDCONS.html

### How to apply a quick fix in the NGINX config
1. ssh to machine running is, e.g. ssh sysadmin@acc.idcons.nl / see pwsafe for password
2. find the appropriate docker container using docker ps -> e.g. 6ce4ae557202
3. edit the file on the host: sudo vi /opt/nginx/config/ssl.idcons.conf
4. restart the container: docker restart 6ce4ae557202

### How to copy data from ACC or PROD to your local laptop
For prod you can use the script docker/axon-restore/restore_from_prod.sh and follow instructions. 
Or you can use docker/axon-restore/restore_backup.sh if you don't want a fresh backup from prod.
Below are the manual instructions:
1. Get a backup from /opt/backup/axondb/ on any database node
	- see pwsafe (get on VPN first!) for url and use sysadmin account
	- e.g. ssh sysadmin@acc-db03.idcons.nl / <see pwsafe>
	- file: /opt/backup/axondb/acc-db03-idcons/axondb-backup-latest.tgz
so: scp sysadmin@acc-db03.idcons.nl:/opt/backup/axondb/acc-db03-idcons/axondb-backup-latest.tgz .

2. Create temp dir unzip and untar this in what is known as the "restore location":  
/Users/wilco/tmp  
Mv *tgz to tmp  
Gunzip  
Untar  
=> e.g. restore_location: /Users/wilco/tmp

2. Prepare local environment by deleting all data
Stop app  
Stop dockers  
docker system prune  
docker volume prune  
Clean Mongo DB if needed (delete all Collections) e.g. by running:
mongo < dropAllCollectionOfLocalMongoDB.js

3. Copy the data from the restore location to your Docker instance running AxonDB
`docker run -i --rm -v docker_axondb:/events -v /Users/wilco/tmp:/restore busybox cp -R /restore/backup/events /`
Verification:
`docker run -i --rm -v docker_axondb:/events -v /Users/wilco/tmp:/restore busybox ls -la /events/default`  
Should show "event" and "snapshot" files

4. Start dockers and wait until your AxonDB is avail. Verify it has events  
http://localhost:8023 -> should show a considerable number of events e.g. 224032 events

5. Start application

6. Replay (see also above):
Use the script docker/replay.sh or execute manually:
curl -XPOST -H "Content-Type: application/json" http://localhost:8080/eventprocessing/replayall -d <replay-token>

7. Track replay progress (see also above):
curl -XPOST -H "Content-Type: application/json" http://localhost:8080/eventprocessing/replayprogress -d <replay-token>

8. Gather statistics on events per user (NB since last restart only as it is an in mem only):
curl -XPOST -H "Content-Type: application/json" http://localhost:8080/eventprocessing/eventstats -d <replay-token>

### How to connect to mongodb acc/prod read/write
1. obtain mongodb from Gitlab secrets e.g. for ACC: uri: mongodb://<user>:<password>@acc-db01.idcons.nl,acc-db02.idcons.nl,acc-db03.idcons.nl:27017/idcons?ssl=true&replicaSet=idcons
2. concat the value of <ACC_MANUAL_SSL_CERT> and <ACC_MANUAL_SSL_KEY> into a single file client.pem
3. put the value of <ACC_MONGODB_SSL_CA_PEM> in a file ca.pem
4. lookup the value of the keystore password <ACC_WEBAPP_KEYSTORE_PASSWORD>
4. connect to mongo db `mongo <URI> --ssl --sslCAFile ca.pem --sslPEMKeyFile client.pem --sslPEMKeyPassword <sslPemKeyPassword>`
5. when you need to drop the whole database, connect as regular user (usually 'idcons') like this: 
mongo mongodb://idcons:<password>@acc-db01.idcons.nl,acc-db02.idcons.nl,acc-db03.idcons.nl:27017/idcons?ssl=true --ssl --sslCAFile ca.pem --sslPEMKeyFile crtkey.pem --sslPEMKeyPassword <sslPemKeyPassword> --sslAllowInvalidCertificates
and use:
> use idcons
Next, drop each collection like:
> db.trackingtokens.drop(); 
see if your done using
> show collections

### How to connect to mongodb dev read/write
1. ssh tunnel to primary db node using the following command `ssh -L localport:hostname:remoteport hostname` for example for vagrant `ssh -L 27017:idcons-db1:27017 idcons-db1`
2. concat the certificate and key using the following command: `cat client.crt client.key > client.pem`
3. connect to the mongo db `mongo localhost:27017 -u <mongoUsername> -p <mongoPass> --authenticationDatabase <authDB> --ssl --sslCAFile ca.cert --sslPEMKeyFile client.pem --sslPEMKeyPassword <sslPemKeyPassword>`

### How to connect to mongodb acc/prod read/write with Compass
1. SSH into a db server (i.e. `ssh sysadmin@acc-db03.idcons.nl`)
2. Exec into the docker container, and retrieve the contents of `ca.pem` and `crtkey.pem` inside the /config folder and save as THREE seperate files (so split up crtkey.pem) on your local machine
   ```
   docker ps -> find mongo container ID/hash
   docker exec -it <mongo container hash> /bin/bash
   cd config
3. Close the previous SSH connection make a new tunneled one (the Compass built-in tunnel does not seem to work):
   ```
   ssh -L 27017:localhost:27017 sysadmin@acc-db03.idcons.nl
4. Input the following settings in Compass:
   ```
   Hostname: localhost
   Port: 27017
   Authentication X.509
   Username: <Leave empty>
   
   More Options ->
   Read Preference: Primary Preferred
   SSL: Server and Client Validation
   Certificate authority: <File created from contents of ca.pem>
   Client certificate: <File created from first part of crtkey.pem>
   Client Private Key <File created from second part of crtkey.pem>
   Client Key Password <Leave empty>
   SSH Tunnel: None
5. Connect!

### How to connect to mongodb acc/prod read/write
1. Obtain mongodb url
2. Copy the ca.pem from the mongodb cluster configuration located at `/opt/mongodb-cluster/config` to the mongo docker image
3. Create crtkey.pem file with the ACC_MANUAL_SSL_CERT & ACC_MANUAL_SSL_KEY env variables.
4. Bash into the mongo docker image in one of the db nodes.
5. Connect to mongo db `mongo mongodb://<user>:<password>@<URL>:<port>/<db>?ssl=true --ssl --sslCAFile ca.pem --sslPEMKeyFile crtkey.pem --sslPEMKeyPassword <WEBAPP_KEYSTORE_PASSWORD>`
   (for the values of url/ port /db / user / password / WEBAPP_KEYSTORE_PASSWORD see the secrets)
So steps are:
   ssh sysadmin@acc-db01.idcons.nl
   docker ps
   docker exec -ti <image> bash
   cd /opt
   mongo mongodb:....
within mongo yiou should see PRIMARY as prompt (usually node 01). Then e.g.
> use idcons
> show collections
> db.personEntry.drop()

### How to replace self signed certificates (For Mongodb nodes connection, WebApp to Mongodb connection & Manual operations connections)

1. Generate and save certs for the environment using `deployment/ssl/selfsigned/generate_mongodb_webapp_manual_certs.sh`  
2. Save MANUAL_OPS certs locally or in your password manager.
3. Change <env>_WEBAPP_SSL_CERT, <env>_WEBAPP_SSL_KEY & <env>_WEBAPP_KEYSTORE_PASSWORD env variables
4. Change <env>_MONGODB_SSL_CERT, <env>_MONGODB_SSL_KEY & <env>_MONGODB_SSL_CA_PEM env variables
5. spring.data.mongodb.uri should contain ?ssl=true

### How to replace client facing certificates from external certificate authority
1. Extract the certificates provided
2. Replace the  <env>_IDCONS_SSL_CA_PEM, <env>_IDCONS_SSL_KEY & <env>_IDCONS_SSL_CERT

**As from 0540c2e9f236d0229f7b02950a3beb057ee73bfb <env>_IDCONS_SSL_CRTKEY_PEM is conctructed through the concatination of <env>_IDCONS_SSL_CERT & <env>_IDCONS_SSL_KEY. This does not need to be in the enviorment variables anymore.**

### How to replace Axon snapshot files
We ran into trouble when serializing a snapshot for an aggregate without getters. The symptoms were:
- when updating an entity, you get Axon Exception "IncompatibleAggregateException: Aggregate identifier must be non-null after applying an event. Make sure the aggregate identifier is initialized at the latest when handling the creation event.".
- NOT all instances of the same entity suffer from this problem
- creating a new instance of the entity succeeds and you can happily update it too, even more than 50 updates (which is the snapshot trigger level) all succeed, unless the application is restarted (caches are cleared), and you try to update the aggregate

So, when somehow snapshots are corrupt or you want to start with a clean slate, and you already tested this locally, then act as follows for ACC/PROD clusters:
  - run a backup
  - stop the application on the central HOST (docker stop <image>)
   - ssh to all DB nodes as sysadmin and stop the docker instances running Axon
   - when ALL those Axon dockers are stopped and you are still on the DB host, then fire
      `docker run --rm -it -v axondb-cluster_axondb-data:/data/ ubuntu /bin/bash`
   - you are now running 'bash' on a temporary ubuntu image which has the Axon data mounted
   - on that image, go to the Axon data directory:
     `cd /data/events/default`
   - delete all *.snapshot files
   - `exit` to leave the temporary docker image and return to the DB host
   - repeat deletion for all Axon nodes
   - when ALL Axon dockers are cleaned up this way, start them up again one by one (docker start <image>)
   - finally start the docker image running the application
   - log onto the system using a browser as usual 
   - VERIFY on the DB host and Axon docker image that *.snapshot files are re-created
It could be that the application appears ill responsive for a while. This is due to Axon re-creating its snapshots. 

### How to update OR-tools
1. Java-code jar
   1. Go to github: https://github.com/google/or-tools/releases
   1. Download Ubuntu binary version of or-tools (or-tools_ubuntu-20.10_v8.1.8487.tar.gz)
   1. Extract
   1. Copy ortools-java-{version}.jar to idcons/lib
   1. Copy pom_local.xml to idcons/lib/ortools-pom.xml
   1. Edit install.sh and change the pointer to the new jar-file
   1. Run install.sh
   1. Rebuild back-end: ```mvn clean install -Dskip.unit.tests=true -pl back-end```
1. Native linux libraries
   1. Download java_linux.tar.gz
   1. Extract   
   1. Copy libortools.so and libjniortools.so from within the ortools-linux-x86-64-{version}.jar to idcons/lib/native/
1. Native windows libraries
   1 Download java_win.zip
   1. Extract
   1. Copy jniortools.dll from within the ortools-wis32-x86-64-{version}.jar to idcons/lib/native/
1. Native OSX libraries
   1. Download java_osx.zip
   1. Extract
   1. Copy libjniortools.dylib and libortools.dylib from within the ortools-darwin-{version}.jar to idcons/lib/native/

### How to analyse event handling performance
The CustomEventListenerLoggingInterceptor logs (INFO) the execution time of every event being handled by a listener. This information can be used to pin-point the slower event-handling logic. Below are some shell oneliners that make analysing this data easy
These one-liners do assume a log-file exists containing the log-errors. In the run-configuration in IntelliJ you can configure a log-file for the application. To analyse all events it's necessary to run a replay first.

##### execution time per individual event handled
Output: Linenumber, listener class name, event class name, aggregate identifier, execution time (ms) with the highest execution time on top
```shell
grep -r executionTime -n logs/console.log | awk '{p=index($1, ":"); print substr($1, 0, p-1) " " $12 " " $15 " " $17 " " substr($21, 0, length($21)-2)}' | sort -n -k5 -r | less
```

##### Total execution time spent per listener class and event class combination
Output: Listener class name combined with event class name, summed execution time (ms) with the highest summed execution time on top
```shell
grep -r executionTime -n logs/console.log | awk '{p=index($1, ":"); print substr($1, 0, p-1) " " $12 " " $15 " " $17 " " substr($21, 0, length($21)-2)}' | sort -n -k5 -r | awk '{a[$2 $3] += $5} END { for (i in a) {print i ": " a[i]}}' | sort -n -k2 -r | less
```
</div>		
