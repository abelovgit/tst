<link rel="stylesheet" href="https://abelovgit.github.io/tst/styles.css" />

# idcons rulezzzz

# Table of contents
* [Repository Structure](#repository-structure)
* [Environments](#environments)
* [Databases](#databases)
* <details markdown="1"> <summary> <a href="#running-locally"> Running locally </a> </summary> 
  
  * [Step 1 - Configure Maven](#step1_maven) 
  * [Step 2 - Setup Mongo DB](#step2_mongo)  
  * [Step 3 - Configure IntelliJ IDEA](#step3_idea)
  * [Step 4 - Build application](#step4_build)
  * [Step 5 - Copy Axon DB](#step5_copy_db)
  * [Step 6 - Run Docker](#step6_docker)
 
 </details>
 
* [Debug](#debug)
* <details markdown="1"> <summary> <a href="#faq"> FAQ </a> </summary>

   * [How do I make a change to what is in production?](#how-do-i-make-a-change-to-what-is-in-production)
   * [How do I take something which is already fixed on master (or another source branch) to production without taking along other commits already on master?](#how-do-i-take-something-which-is-already-fixed)
   
<!--    * [How to replay events](#how-to-replay-events)
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
   * [How to analyse event handling performance](#how-to-analyse-event-handling-performance) -->
 </details>
 


<div id="repository-structure" class="tab-content">
<details open markdown="1">
<summary> <b> Repository Structure </b> </summary>

Important elements of the repository are explained bellow:
<pre>
|--pom.xml     --> configuration of modules and dependencies
|--application --> responsible for creation of Spring Boot WebApplication
|--back-end    --> back-end part of the application
|--client-api  --> classes for communication with trading platform(s)
|--common      --> libraries shared by multiple projects
|--deployment  --> tools and configs for local deployment of the application
|--docker      --> scripts for running docker containers, replay of AxonDB events, etc.
|  |--axon-restore --> scripts for copying AxonDB and its local restoration  
|
|--docs        --> documentation
|--etpa-client --> classes specific for ETPA trading platform 
|--front-end   --> javascript front-end of the application
|--lib         --> package with `oortools` optimization solver

</pre>
  
For detailed documentation about the environment refer to [Confluence page](https://gopacs.atlassian.net/wiki/home).

[Back to contents](#table-of-contents)

</details>

</div>

<!--++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-->
<div id="environments" class="tab-content" markdown="1">
<details open markdown="1">
<summary> <b> Environments </b> </summary>
 
| Environment | Branches        | Links                                                                                                                              |
|-------------|-----------------|-------------------------------------------------------------------------------------------------------------------------------------|
| Test        | any (manual)    | [APP](https://tst.idcons.nl),[LOGS](https://tst.idcons.nl:5601),[METRICS](https://tst.idcons.nl:3000/)                              |
| Acceptance  | master (manual) | [APP](https://acc.idcons.nl),[LOGS](https://acc-monitoring.idcons.nl:5601),[METRICS](https://acc-monitoring.idcons.nl:3000/)        |
| Production  | master (manual) | [APP](https://idcons.nl),[LOGS](https://monitoring.idcons.nl:5601),[METRICS](https://monitoring.idcons.nl:3000/) 
 
NOTES: 
* Credentials can be found on https://pwsafe.trifork.nl
* OTP can be generated at https://totp.danhersam.com/

[Previous](#repository-structure) | [Back to contents](#table-of-contents)

</details>

</div>

<!--++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-->
<div id="databases" class="tab-content">
<details open markdown="1">
<summary> <b> Databases </b> </summary>

| Environment | SSH Tunnel                                                                       | Links                                                                |
|-------------|----------------------------------------------------------------------------------|----------------------------------------------------------------------|
| Test        | `ssh -L 8443:localhost:8443 -L 8081:localhost:8081 sysadmin@tst.idcons.nl`       | [MONGODB](https://localhost:8081/),[AXONDB](https://localhost:8443/) |
| Acceptance  | `ssh -L 8443:localhost:8443 -L 8081:localhost:8081 sysadmin@acc-db01.idcons.nl`  | [MONGODB](https://localhost:8081/),[AXONDB](https://localhost:8443/) |  
| Production  | `ssh -L 8443:localhost:8443 -L 8081:localhost:8081 sysadmin@db01.idcons.nl`      | [MONGODB](https://localhost:8081/),[AXONDB](https://localhost:8443/) |

For Mongo Acceptance, set up the tunnel, go to the link and use user 'idcons_ro' 

NOTES: 
* Credentials can be found on https://pwsafe.trifork.nl
* Establish the SSH tunnel before attempting to visit the prescribed ports on localhost

[Previous](#environments) | [Back to contents](#table-of-contents)

</details>

</div>

<!--++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-->
<!-- <div id="running-locally">  -->

### Running locally

<details open id="step1_maven">
<summary> <b> Step 1 - Configure Maven </b> </summary> 

In the local repository, run `./lib/install.sh` in order to install a missing dependency.

[Previous](#databases) | [Back to contents](#table-of-contents)   

</details>  

<details open id="step2_mongo">
<summary> <b> Step 2 - Setup Mongo DB </b> </summary>    

Setup VMs for Mongo DB cluster locally: <br/>    
1. Download Vagrant and Virtualbox for your OS <br/>
2. Run `deployment/vagrant/recreate.sh` <br/>
3. If not yet the case, add `Include config.d/*` as the FIRST line into `~/.ssh/config <br/>
4. Run `deployment/ansible/run.sh vagrant` to populate the VMs <br/>
5. Run `vagrant status` inside the `vagrant` folder to retrieve hostnames <br/>

Note: 
* To check that VMs are installed properly, connect to one of them using for example: `ssh idcons-db1` <br/>
* Use `vagrant up` to turn on the installed VMs <br/>
       
 [Previous](#step1_maven) | [Back to contents](#table-of-contents)
          
</details>  
    
<details id="step3_idea" open>
<summary> <b> Step 3 - Configure IntelliJ IDEA </b> </summary> 

Navigate to IntelliJ IDEA run config:
         
![image](https://user-images.githubusercontent.com/89839322/131587909-464d89bd-149d-44f1-9501-2749ee1d16a3.png)
         
Set VM options:     
```
-Djava.library.path=./lib/native
```
 Set the following to the active profiles:
```
dev
```
as shown in ![image](https://user-images.githubusercontent.com/89839322/131588402-545653c0-d79d-491e-8423-c4506a9aa324.png)   

[Previous](#step2_mongo) | [Back to contents](#table-of-contents)   

</details>   

<details id="step4_build" open>
<summary> <b> Step 4 - Build application </b> </summary> 

Build the application by running:
```
./build.sh
```
Tap into the application by running it via GUI
       
![image](https://user-images.githubusercontent.com/89839322/131589340-c2705e13-6a40-44d7-bf9d-4839b079d185.png)
       
and by navigating to `https://localhost:8080`.
       
You should be able to see the following screen
       
![image](https://user-images.githubusercontent.com/89839322/131589729-d19d00ec-2c96-4a98-8e16-254952c8454d.png)
       
At this point, Mongo DB is empty and should be restored from PRD. Stop the application in IDEA by clicking "Stop" button. 

[Previous](#step3_idea) | [Back to contents](#table-of-contents)   

</details>    
    
<details id="step5_copy_db" open>
<summary> <b> Step 5 - Copy Axon DB </b> </summary> 

1. Run `./docker/axon-restore/get_backup_prod.sh` in order to copy DB (PROD) to local drive.</li>
2. Execute `./docker/axon-restore/restore_backup.sh` and follow the provided instructions.</li>   
3. Launch `./docker/replay.sh' to replay AxonDB events locally.</li>
4. Trigger `./docker/admin_disable_2fa.sh` to reset 2FA in order to be able to reset admin password.</li>   

[Previous](#step4_build) | [Back to contents](#table-of-contents)   

</details>     
 
<details id="step6_docker" open>
<summary> <b> Step 6 - Run Docker </b> </summary> 

1. Run `./docker/run.sh wo` to start the containers.</li>
2. Tap into the application again at `https://localhost:8080` to reset the password for 'admin' user.</li>   
3. After reseting the admin password, login to IDCONS admin dashboard and create a new user (or change the password of existing one).</li>  
4. You should receive a link for password reset in the local mailcatcher `http://localhost:1080`</li> 
5. You should be able to login under the desired user now.</li>  

[Previous](#step5_copy_db) | [Back to contents](#table-of-contents)   

</details>
    

<!--++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-->

<div id="debug" class="tab-content">
<details open markdown="1">
<summary> <b> Debug </b> </summary>
  
Use the konami code to activate UI debugging: up, up, down, down, left, right, left, right, b, a `https://en.wikipedia.org/wiki/Konami_Code`.

[Previous](#running-locally) | [Back to contents](#table-of-contents)

</details>

</div>

<!--++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-->

<div id="faq" class="tab-content" markdown="1">
<details open markdown="1">
<summary> <b> FAQ </b> </summary>

  <div style="margin: 10px;">
      <details  open id="how-do-i-make-a-change-to-what-is-in-production">
      <summary> <b> How do I make a change to what is in production? </b> </summary>

      1. Check out the commit which is currently in prd: <br/>```git checkout <current_version_in_prd>```<br/>
      2. Make a branch of it starting with "HOTFIX-": <br/>```git checkout -b HOTFIX-<name>```<br/>
      3. Make, commit and push your changes:<br/>
      ```<make changes>```<br/>
      ```git add -A```<br/>
      ```git commit```<br/>
      ```git push```<br/>
      4. Run the gitlab pipeline jobs the same way you would for the master branch.

      </details>
        
  </div>
      
      <!--+++++++++++++++++++++++++++++++++++-->
  <div style="margin: 10px;">
      <details  open id="how-do-i-take-something-which-is-already-fixed">
      <summary> <b> How do I take something which is already fixed on master (or another source branch) to production without taking along other commits already on master? </b> </summary>

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
      
      </details>   
        
  </div>        
      
       <!--+++++++++++++++++++++++++++++++++++-->

[Previous](#debug) | [Back to contents](#table-of-contents)

</details>

</div>
