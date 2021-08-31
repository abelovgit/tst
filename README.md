<link rel="stylesheet" href="https://abelovgit.github.io/tst/styles.css" />

# idcons rulezzzz

# Table of contents
* [Repository Structure](#repository-structure)
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
<!--* [How to connect to mongodb acc/prod read/write (2)](#how-to-connect-to-mongodb-accprod-readwrite-2)-->
* [How to replace self signed certificates (For Mongodb nodes connection, WebApp to Mongodb connection & Manual operations connections)](#how-to-replace-self-signed-certificates-for-mongodb-nodes-connection-webapp-to-mongodb-connection--manual-operations-connections)
* [How to replace client facing certificates from external certificate authority](#how-to-replace-client-facing-certificates-from-external-certificate-authority)
* [How to replace Axon snapshot files](#how-to-replace-axon-snapshot-files)
* [How to update OR-tools](#how-to-update-or-tools)
* [How to analyse event handling performance](#how-to-analyse-event-handling-performance)


<div id="repository-structure" class="tab-content" markdown="1">
<details open markdown="1">
<summary> <b> Repository Structure </b> </summary>

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
* Credentials can be found on [](https://pwsafe.trifork.nl)
* OTP can be generated at [](https://totp.danhersam.com/)

[Previous](#repository-structure) | [Back to contents](#table-of-contents)

</details>

</div>

<!--++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-->
<div id="databases" class="tab-content" markdown="1">
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
<div id="running-locally" class="tab-content" markdown="1">
<details open markdown="1">
<summary> <b> Running locally </b> </summary> 
 
<div class="tabbed-area adjacent" markdown="1">
   <div id="box-thirteen" markdown="1">
      #### Maven
       Before building with Maven you need to add the missing dependency to the local repository:
       ```
       ./lib/install.sh
       ```
   </div>
 
   <div id="box-fourteen" markdown="1">
   <p>Feugiat vitae, ultricies eget, tempor sit amet, ante. Donec eu libero sit amet quam egestas semper. Aenean ultricies mi vitae est. Mauris placerat eleifend leo. Quisque sit amet est et sapien ullamcorper pharetra. Vestibulum erat wisi, condimentum sed, commodo vitae, ornare sit amet, wisi. Aenean fermentum, elit eget tincidunt condimentum, eros ipsum rutrum orci, sagittis tempus lacus enim ac dui. Donec non enim in turpis pulvinar facilisis. Ut felis. Praesent dapibus, neque id cursus faucibus, tortor neque egestas augue, eu vulputate magna eros eu erat. Aliquam erat volutpat. Nam dui mi, tincidunt quis, accumsan porttitor, facilisis luctus, metus</p>
   </div>
 
   <ul class="tabs group">
    <li><a href="#box-thirteen">Step 1</a></li>
   <li><a href="#box-fourteen">Step 2</a></li>
   </ul>
</div>
 

<!-- <div class="w3c" markdown="span">
   <div id="tab16" markdown="span">
     <a href="#tab16">Step 1</a>
     <div markdown="span">
      #### Maven
       Before building with Maven you need to add the missing dependency to the local repository:
       ```
       ./lib/install.sh
       ```
     </div>
   </div>

   <div id="tab17" markdown="1">
     <a href="#tab17">Step 2</a>
     <div markdown="1">
         <h4> Using Vagrant </h4>     
         You can mimic cluster setup for mongo etc locally by using vagrant and virtualbox, Steps needed are:
         * Download Vagrant and Virtualbox for your OS
         * Run `deployment/vagrant/recreate.sh` 
         * If not yet the case, add `Include config.d/*` as the FIRST line of ~/.ssh/config
         * Use Ansible to populate the VMs using `deployment/ansible/run.sh vagrant`
         * Run `vagrant status` inside the `vagrant` folder to retrieve hostnames, then connect to one of the instances using for example: `ssh idcons-db1`
         <div markdown="1">
            To use existing VMs instead of recreating altogether (much faster after the first time), use `vagrant up` or just keep them running
         </div>
     </div>
   </div>

</div> -->

</details>

</div>




