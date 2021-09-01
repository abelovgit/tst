<link rel="stylesheet" href="https://abelovgit.github.io/tst/styles.css" />

# idcons rulezzzz

# Table of contents
* [Repository Structure](#repository-structure)
* [Environments](#environments)
* [Databases](#databases)
<details markdown="1">
<summary> <a href="#running-locally"> Running locally </a> </summary> 
  
  * [Maven](#step1_maven) 
  * [Mongo DB](#step2_mongo)  
  * [IDEA](#step3_idea)
  * [Command Line](#command-line)
  * [Setup Initial Data](#setup-initial-data)
  * [Docker](#docker)
  * [Mail service](#mail-service)  
  
 </details>
 
* [Debug](#debug)

<details markdown="1">
<summary> <a href="#faq"> FAQ </a> </summary>

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
<!-- <div id="running-locally" class="tab-content"> -->
<!-- <details open>
<summary> <b> Running locally </b> </summary>  -->
  
  <p> <b> Running locally </b> </p>
 
<!-- <div class="tabbed-area adjacent" markdown="1">
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
</div> -->
 

<div class="w3c">
   <div id="step1_maven">
      <a href="#step1_maven" style="color: black;"> <b> Step 1 - Maven </b> </a>
      <div>
       In the local repository, run `./lib/install.sh` in order to install a missing dependency.
        [Previous](#databases) | [Back to contents](#table-of-contents)     
      </div>
   </div>

   <div id="step2_mongo">
      <a href="#step2_mongo" style="color: black;"> <b> Step 2 - Mongo DB </b> </a>
      <div>
         Setup VMs for Mongo DB cluster locally:     
       <ol>
           <li> Download Vagrant and Virtualbox for your OS </li>
           <li> Run `deployment/vagrant/recreate.sh` </li>
           <li> If not yet the case, add `Include config.d/*` as the FIRST line into ~/.ssh/config </li>
           <li> Run `deployment/ansible/run.sh vagrant` to populate the VMs </li>
           <li> Run `vagrant status` inside the `vagrant` folder to retrieve hostnames </li>
       </ol>
          Note: 
       <ul>
           <li> To check that VMs are installed properly, connect to one of them using for example: `ssh idcons-db1` </li>
           <li> Use `vagrant up` to turn on the installed VMs. </li>
       </ul> 
       [Previous](#step1_maven) | [Back to contents](#table-of-contents)  
      </div>
   </div>
 
   <div id="step3_idea">
      <a href="#step3_idea" style="color: black;"> <b> Step 3 - IntelliJ IDEA </b> </a>
      <div>
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
       as shown in 
       ![image](https://user-images.githubusercontent.com/89839322/131588402-545653c0-d79d-491e-8423-c4506a9aa324.png)
        [Previous](#databases) | [Back to contents](#table-of-contents)     
      </div>
   </div> 
 
   <div id="step4_build">
      <a href="#step4_build" style="color: black;"> <b> Step 4 - Build </b> </a>
      <div>
       Build the application by running:
        ```
        ./build.sh
        ```
       Tap into the application by running it via GUI
       ![image](https://user-images.githubusercontent.com/89839322/131589340-c2705e13-6a40-44d7-bf9d-4839b079d185.png)
       and by navigating to `https://localhost:8080`.
       You should be able to see the following screen
       ![image](https://user-images.githubusercontent.com/89839322/131589729-d19d00ec-2c96-4a98-8e16-254952c8454d.png)
       At this point, Mongo DB is empty and should be restored from PRD. Stop the application in IDEA by clicking "stop" button.
        [Previous](#databases) | [Back to contents](#table-of-contents)     
      </div>
   </div> 
 
   <div id="step5_copy_db">
      <a href="#step5_copy_db" style="color: black;"> <b> Step 5 - Copy DB </b> </a>
      <div>
      <ol>
       <li> Run `./docker/axon-restore/get_backup_prod.sh` in order to copy DB (PROD) to local drive.</li>
       <li> Execute `./docker/axon-restore/restore_backup.sh` and follow the provided instructions.</li>   
       <li> Launch `./docker/replay.sh' to replay AxonDB events locally.</li>
       <li> Trigger './docker/admin_disable_2fa.sh' to reset 2FA in order to be able to reset admin password.</li>
       </ol>
        [Previous](#databases) | [Back to contents](#table-of-contents)         
      </div>
   </div> 
 
   <div id="step6_docker">
      <a href="#step6_docker" style="color: black;"> <b> Step 6 - Docker </b> </a>
      <div>
      <ol>
       <li> Run `./docker/run.sh wo` to start the container.</li>
       <li> Tap into the application again at `https://localhost:8080` to reset the password for 'admin' user.</li>   
       <li> After reseting the admin password, login to IDCONS admin dashboard and create a new user (or change the password of existing one).</li>  
       <li> You should receive a link for password reset in ocal mailcatcher `http://localhost:1080`</li> 
       <li> You should be able to login under the desired user now.</li>  
       </ol>
        [Previous](#databases) | [Back to contents](#table-of-contents)         
      </div>
   </div>  
  
</div>

<!-- </details> -->

<!-- </div>  -->

<!--++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++-->

<div id="debug" class="tab-content" markdown="1">
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
