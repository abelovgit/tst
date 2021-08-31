<h1 class="code-line" data-line-start=0 data-line-end=1 ><a id="idcons_rulezzzz_0"></a>idcons rulezzzz</h1>
<h2 class="code-line" data-line-start=2 data-line-end=3 ><a id="Table_of_contents_tableofcontents_2"></a>Table of contents {#table-of-contents}</h2>
<ul>
<li class="has-line-data" data-line-start="3" data-line-end="4"><a href="#environments">Environments</a></li>
<li class="has-line-data" data-line-start="4" data-line-end="5"><a href="#databases">Databases</a></li>
<li class="has-line-data" data-line-start="5" data-line-end="13"><a href="#running-locally">Running locally</a>
<ul>
<li class="has-line-data" data-line-start="6" data-line-end="7"><a href="#maven">Maven</a></li>
<li class="has-line-data" data-line-start="7" data-line-end="8"><a href="#using-vagrant">Using Vagrant</a></li>
<li class="has-line-data" data-line-start="8" data-line-end="9"><a href="#idea">IDEA</a></li>
<li class="has-line-data" data-line-start="9" data-line-end="10"><a href="#command-line">Command Line</a></li>
<li class="has-line-data" data-line-start="10" data-line-end="11"><a href="#setup-initial-data">Setup Initial Data</a></li>
<li class="has-line-data" data-line-start="11" data-line-end="12"><a href="#docker">Docker</a></li>
<li class="has-line-data" data-line-start="12" data-line-end="13"><a href="#mail-service">Mail service</a></li>
</ul>
</li>
<li class="has-line-data" data-line-start="13" data-line-end="14"><a href="#debug">Debug</a></li>
<li class="has-line-data" data-line-start="14" data-line-end="17"><a href="#hotfixes">Hotfixes</a>
<ul>
<li class="has-line-data" data-line-start="15" data-line-end="16"><a href="#how-do-i-make-a-change-to-what-is-in-production">How do I make a change to what is in production?</a></li>
<li class="has-line-data" data-line-start="16" data-line-end="17"><a href="#how-do-i-take-something-which-is-already-fixed-on-master-or-another-source-branch-to-production-without-taking-along-other-commits-already-on-master">How do I take something which is already fixed on master (or another source branch) to production without taking along other commits already on master?</a></li>
</ul>
</li>
<li class="has-line-data" data-line-start="17" data-line-end="18"><a href="#how-to-replay-events">How to replay events</a></li>
<li class="has-line-data" data-line-start="18" data-line-end="19"><a href="#how-to-generate-etpa-orders-in-acc-environment">How to generate ETPA orders in ACC environment</a></li>
<li class="has-line-data" data-line-start="19" data-line-end="20"><a href="#how-to-apply-a-quick-fix-in-the-nginx-config">How to apply a quick fix in the NGINX config</a></li>
<li class="has-line-data" data-line-start="20" data-line-end="21"><a href="#how-to-copy-data-from-acc-or-prod-to-your-local-laptop">How to copy data from ACC or PROD to your local laptop</a></li>
<li class="has-line-data" data-line-start="21" data-line-end="22"><a href="#how-to-connect-to-mongodb-accprod-readwrite">How to connect to mongodb acc/prod read/write</a></li>
<li class="has-line-data" data-line-start="22" data-line-end="23"><a href="#how-to-connect-to-mongodb-dev-readwrite">How to connect to mongodb dev read/write</a></li>
<li class="has-line-data" data-line-start="23" data-line-end="24"><a href="#how-to-connect-to-mongodb-accprod-readwrite-2">How to connect to mongodb acc/prod read/write (2)</a></li>
<li class="has-line-data" data-line-start="24" data-line-end="25"><a href="#how-to-replace-self-signed-certificates-for-mongodb-nodes-connection-webapp-to-mongodb-connection--manual-operations-connections">How to replace self signed certificates (For Mongodb nodes connection, WebApp to Mongodb connection &amp; Manual operations connections)</a></li>
<li class="has-line-data" data-line-start="25" data-line-end="26"><a href="#how-to-replace-client-facing-certificates-from-external-certificate-authority">How to replace client facing certificates from external certificate authority</a></li>
<li class="has-line-data" data-line-start="26" data-line-end="27"><a href="#how-to-replace-axon-snapshot-files">How to replace Axon snapshot files</a></li>
<li class="has-line-data" data-line-start="27" data-line-end="28"><a href="#how-to-update-or-tools">How to update OR-tools</a></li>
<li class="has-line-data" data-line-start="28" data-line-end="30"><a href="#how-to-analyse-event-handling-performance">How to analyse event handling performance</a></li>
</ul>
<h3 class="code-line" data-line-start=30 data-line-end=31 ><a id="Environments_30"></a>Environments</h3>
<table class="table table-striped table-bordered">
<thead>
<tr>
<th>Environment</th>
<th>Branches</th>
<th>Links</th>
</tr>
</thead>
<tbody>
<tr>
<td>Test</td>
<td>any (manual)</td>
<td><a href="https://tst.idcons.nl">APP</a>,<a href="https://tst.idcons.nl:5601">LOGS</a>,<a href="https://tst.idcons.nl:3000/">METRICS</a></td>
</tr>
<tr>
<td>Acceptance</td>
<td>master (manual)</td>
<td><a href="https://acc.idcons.nl">APP</a>,<a href="https://acc-monitoring.idcons.nl:5601">LOGS</a>,<a href="https://acc-monitoring.idcons.nl:3000/">METRICS</a></td>
</tr>
<tr>
<td>Production</td>
<td>master (manual)</td>
<td><a href="https://idcons.nl">APP</a>,<a href="https://monitoring.idcons.nl:5601">LOGS</a>,<a href="https://monitoring.idcons.nl:3000/">METRICS</a></td>
</tr>
</tbody>
</table>
<p class="has-line-data" data-line-start="37" data-line-end="38">NOTES:</p>
<ul>
<li class="has-line-data" data-line-start="38" data-line-end="39">Credentials can be found on <a href="https://pwsafe.trifork.nl">https://pwsafe.trifork.nl</a></li>
<li class="has-line-data" data-line-start="39" data-line-end="41">OTP can be generated at <a href="https://totp.danhersam.com/">https://totp.danhersam.com/</a></li>
</ul>
<h3 class="code-line" data-line-start=41 data-line-end=42 ><a id="DATABASES_databases_41"></a>DATABASES {#databases}</h3>
<table class="table table-striped table-bordered">
<thead>
<tr>
<th>Environment</th>
<th>SSH Tunnel</th>
<th>Links</th>
</tr>
</thead>
<tbody>
<tr>
<td>Test</td>
<td><code>ssh -L 8443:localhost:8443 -L 8081:localhost:8081 sysadmin@tst.idcons.nl</code></td>
<td><a href="https://localhost:8081/">MONGODB</a>,<a href="https://localhost:8443/">AXONDB</a></td>
</tr>
<tr>
<td>Acceptance</td>
<td><code>ssh -L 8443:localhost:8443 -L 8081:localhost:8081 sysadmin@acc-db01.idcons.nl</code></td>
<td><a href="https://localhost:8081/">MONGODB</a>,<a href="https://localhost:8443/">AXONDB</a></td>
</tr>
<tr>
<td>Production</td>
<td><code>ssh -L 8443:localhost:8443 -L 8081:localhost:8081 sysadmin@db01.idcons.nl</code></td>
<td><a href="https://localhost:8081/">MONGODB</a>,<a href="https://localhost:8443/">AXONDB</a></td>
</tr>
</tbody>
</table>
<p class="has-line-data" data-line-start="48" data-line-end="49">For Mongo Acceptance, set up the tunnel, go to the link and use user ‘idcons_ro’</p>
<p class="has-line-data" data-line-start="50" data-line-end="51">NOTES:</p>
<ul>
<li class="has-line-data" data-line-start="51" data-line-end="52">Credentials can be found on <a href="https://pwsafe.trifork.nl">https://pwsafe.trifork.nl</a></li>
<li class="has-line-data" data-line-start="52" data-line-end="54">Establish the SSH tunnel before attempting to visit the prescribed ports on localhost</li>
</ul>
<p class="has-line-data" data-line-start="54" data-line-end="55"><a href="#table-of-contents">Go up</a></p>
<h3 class="code-line" data-line-start=56 data-line-end=57 ><a id="Running_locally_56"></a>Running locally</h3>
<h5 class="code-line" data-line-start=58 data-line-end=59 ><a id="Maven_58"></a>Maven</h5>
<p class="has-line-data" data-line-start="59" data-line-end="60">Before building with Maven you need to add the missing dependency to the local repository:</p>
<pre><code class="has-line-data" data-line-start="61" data-line-end="63">./lib/install.sh
</code></pre>
<h5 class="code-line" data-line-start=64 data-line-end=65 ><a id="Using_Vagrant_64"></a>Using Vagrant</h5>
<p class="has-line-data" data-line-start="65" data-line-end="66">You can mimic cluster setup for mongo etc locally by using vagrant and virtualbox, Steps needed are:</p>
<ul>
<li class="has-line-data" data-line-start="66" data-line-end="67">Download Vagrant and Virtualbox for your OS</li>
<li class="has-line-data" data-line-start="67" data-line-end="68">Run <code>deployment/vagrant/recreate.sh</code></li>
<li class="has-line-data" data-line-start="68" data-line-end="69">If not yet the case, add <code>Include config.d/*</code> as the FIRST line of ~/.ssh/config</li>
<li class="has-line-data" data-line-start="69" data-line-end="70">Use Ansible to populate the VMs using <code>deployment/ansible/run.sh vagrant</code></li>
<li class="has-line-data" data-line-start="70" data-line-end="72">Run <code>vagrant status</code> inside the <code>vagrant</code> folder to retrieve hostnames, then connect to one of the instances using for example: <code>ssh idcons-db1</code></li>
</ul>
<p class="has-line-data" data-line-start="72" data-line-end="73">To use existing VMs instead of recreating altogether (much faster after the first time), use <code>vagrant up</code> or just keep them running</p>
<h5 class="code-line" data-line-start=74 data-line-end=75 ><a id="IDEA_74"></a>IDEA</h5>
<p class="has-line-data" data-line-start="75" data-line-end="76">Add VM options in intellij run config:</p>
<pre><code class="has-line-data" data-line-start="77" data-line-end="79">-Djava.library.path=./lib/native
</code></pre>
<p class="has-line-data" data-line-start="79" data-line-end="80">Add the following to the active profiles intellij run config:</p>
<pre><code class="has-line-data" data-line-start="81" data-line-end="83">dev
</code></pre>
<h5 class="code-line" data-line-start=84 data-line-end=85 ><a id="Command_Line_84"></a>Command Line</h5>
<pre><code class="has-line-data" data-line-start="86" data-line-end="88">./build.sh &amp;&amp; ./run
</code></pre>
<h5 class="code-line" data-line-start=90 data-line-end=91 ><a id="Setup_Initial_Data_90"></a>Setup Initial Data</h5>
<p class="has-line-data" data-line-start="91" data-line-end="92">Some non prod test data:</p>
<pre><code class="has-line-data" data-line-start="93" data-line-end="95">curl -XPOST http://localhost:8080/setup
</code></pre>
<p class="has-line-data" data-line-start="96" data-line-end="97">Initial prod data:</p>
<pre><code class="has-line-data" data-line-start="98" data-line-end="100">curl -XPOST http://localhost:8080/setupproduction
</code></pre>
<h5 class="code-line" data-line-start=101 data-line-end=102 ><a id="Docker_101"></a>Docker</h5>
<p class="has-line-data" data-line-start="102" data-line-end="103">For one time only to pull AxonDB image from private registry login with below command.</p>
<pre><code class="has-line-data" data-line-start="104" data-line-end="111" class="language-bash">docker login gitlab.etpa.nl:<span class="hljs-number">4567</span>
In <span class="hljs-keyword">case</span> you get a message like this:
 Error response from daemon: Get https://gitlab.etpa.nl:<span class="hljs-number">4567</span>/v2/: unauthorized: HTTP Basic: Access denied\nYou must use a personal access token with ‘api’ scope <span class="hljs-keyword">for</span> Git over HTTP.\nYou can generate one at https://gitlab.etpa.nl/profile/personal_access_tokens
Then go to https://gitlab.etpa.nl/profile/personal_access_tokens and generate a token with <span class="hljs-string">'api'</span> scope. Next,
Try with:
docker login gitlab.etpa.nl:<span class="hljs-number">4567</span> -u &lt;yourusername&gt; -p &lt;the generated token&gt;
</code></pre>
<p class="has-line-data" data-line-start="111" data-line-end="112">Get into docker directory in project and execute run script with ‘wo’ argument. ‘wo’ argument implies ‘without application’.</p>
<pre><code class="has-line-data" data-line-start="113" data-line-end="116" class="language-bash"><span class="hljs-built_in">cd</span> docker
./run.sh wo
</code></pre>
<p class="has-line-data" data-line-start="116" data-line-end="117">If you want to run application and all databases containerized, get into docker directory in project and execute run script with ‘w’ argument. ‘w’ argument implies ‘with application’.</p>
<pre><code class="has-line-data" data-line-start="118" data-line-end="121" class="language-bash"><span class="hljs-built_in">cd</span> docker
./run.sh w
</code></pre>
<p class="has-line-data" data-line-start="122" data-line-end="127">Docker basics:<br>
Look for all images, including the stopped images:<br>
docker ps -a<br>
Tail the logs on an image:<br>
docker logs --follow &lt;imageID&gt;</p>
<p class="has-line-data" data-line-start="128" data-line-end="130">Log onto docker instance: (exec for a command send to the image, ’ti’ for terminal, interactive, and ‘bash’ for the shell of course<br>
docker exec -ti docker_axondb_1 bash</p>
<h5 class="code-line" data-line-start=131 data-line-end=132 ><a id="Mail_service_131"></a>Mail service</h5>
<p class="has-line-data" data-line-start="132" data-line-end="135">When using docker/run.sh for local development mailcatcher is available at <a href="http://localhost:1080">http://localhost:1080</a>.<br>
Otherwise you can use ‘fakesmtp’ to catch outgoing emails when running in ‘dev’ mode. Just download and run it on its default port. Don’t forget to start it…(common hickup)<br>
java -jar fakeSMTP-2.0.jar will do, again…don’t forget to start it…(common hickup)</p>
<h3 class="code-line" data-line-start=136 data-line-end=137 ><a id="Debug_136"></a>Debug</h3>
<p class="has-line-data" data-line-start="137" data-line-end="139">Use the konami code to activate UI debugging: up, up, down, down, left, right, left, right, b, a<br>
<a href="https://en.wikipedia.org/wiki/Konami_Code">https://en.wikipedia.org/wiki/Konami_Code</a></p>
<h3 class="code-line" data-line-start=140 data-line-end=141 ><a id="Hotfixes_140"></a>Hotfixes</h3>
<p class="has-line-data" data-line-start="142" data-line-end="143">NB: This is for emergencies only and should never become a frequent activity.</p>
<h5 class="code-line" data-line-start=144 data-line-end=145 ><a id="How_do_I_make_a_change_to_what_is_in_production_144"></a>How do I make a change to what is in production?</h5>
<ol>
<li class="has-line-data" data-line-start="146" data-line-end="147">Check out the commit which is currently in prd: &lt;br/&gt;<code>git checkout &lt;current_version_in_prd&gt;</code>&lt;br/&gt;</li>
<li class="has-line-data" data-line-start="147" data-line-end="148">Make a branch of it starting with “HOTFIX-”: &lt;br/&gt;<code>git checkout -b HOTFIX-&lt;name&gt;</code>&lt;br/&gt;</li>
<li class="has-line-data" data-line-start="148" data-line-end="153">Make, commit and push your changes:&lt;br/&gt;<br>
<code>&lt;make changes&gt;</code>&lt;br/&gt;<br>
<code>git add -A</code>&lt;br/&gt;<br>
<code>git commit</code>&lt;br/&gt;<br>
<code>git push</code>&lt;br/&gt;</li>
<li class="has-line-data" data-line-start="153" data-line-end="155">Run the gitlab pipeline jobs the same way you would for the master branch.</li>
</ol>
<h5 class="code-line" data-line-start=155 data-line-end=156 ><a id="How_do_I_take_something_which_is_already_fixed_on_master_or_another_source_branch_to_production_without_taking_along_other_commits_already_on_master_155"></a>How do I take something which is already fixed on master (or another source branch) to production without taking along other commits already on master?</h5>
<ol>
<li class="has-line-data" data-line-start="157" data-line-end="158">Check out the commit which is currently in prd: &lt;br/&gt;<code>git checkout &lt;current_version_in_prd&gt;</code>&lt;br/&gt;</li>
<li class="has-line-data" data-line-start="158" data-line-end="159">Make a branch of it: &lt;br/&gt;<code>git checkout -b HOTFIX-&lt;name&gt;</code>&lt;br/&gt;</li>
<li class="has-line-data" data-line-start="159" data-line-end="160">Go to your source branch (let’s assume master from here on out): &lt;br/&gt;<code>git checkout master</code>&lt;br/&gt;</li>
<li class="has-line-data" data-line-start="160" data-line-end="161">Interactively rebase onto the version currently in prd: &lt;br/&gt;<code>git rebase -i HOTFIX-&lt;name&gt;</code>&lt;br/&gt;</li>
<li class="has-line-data" data-line-start="161" data-line-end="162">Now delete all but the changes you want to take to prod (or pick something like “skip” if you’re doing it in an IDE).</li>
<li class="has-line-data" data-line-start="162" data-line-end="163">Complete the rebase. You now have a diverged version of master which can not be pushed, but can be used to merge locally.</li>
<li class="has-line-data" data-line-start="163" data-line-end="165">Go back to your hotfix branch:&lt;br/&gt;<br>
<code>git checkout HOTFIX-&lt;name&gt;</code></li>
<li class="has-line-data" data-line-start="165" data-line-end="166">Merge in your special version of master &lt;br/&gt;<code>git merge master</code>&lt;br/&gt; (note that it’s NOT origin/master, just master)&lt;br/&gt;</li>
<li class="has-line-data" data-line-start="166" data-line-end="167">Push your hotfix branch: &lt;br/&gt;<code>git push</code>&lt;br/&gt;</li>
<li class="has-line-data" data-line-start="167" data-line-end="169">Go back and fix your diverged master: &lt;br/&gt;<code>git checkout master</code>&lt;br/&gt; and &lt;br/&gt;<code>git reset --hard origin/master</code>&lt;br/&gt;</li>
</ol>
<p class="has-line-data" data-line-start="169" data-line-end="170">Your master branch is now back to normal and your hotfix branch contains only what’s in prod plus the changes you hand picked during the rebase.</p>
<h3 class="code-line" data-line-start=171 data-line-end=172 ><a id="How_to_replay_events_171"></a>How to replay events</h3>
<p class="has-line-data" data-line-start="172" data-line-end="176">Run docker/replay.sh or execute manually:<br>
Get the appropriate token from the secrets in gitlab. The key is <code>idcons.replayToken</code>.<br>
Stop nginx by ssh’ing into the application server and stopping the nginx docker.<br>
Run the curl command:</p>
<pre><code class="has-line-data" data-line-start="177" data-line-end="179">curl -XPOST -H &quot;Content-Type: application/json&quot;  http://localhost:8080/eventprocessing/replayall -d &quot;&lt;token&gt;&quot;
</code></pre>
<p class="has-line-data" data-line-start="179" data-line-end="180">Start up the nginx docker container again.</p>
<h3 class="code-line" data-line-start=182 data-line-end=183 ><a id="How_to_generate_ETPA_orders_in_ACC_environment_182"></a>How to generate ETPA orders in ACC environment</h3>
<p class="has-line-data" data-line-start="183" data-line-end="185">Use these urls to generate some orders in the ETPA ACC environment if you want to test the clearing of idcons:<br>
<a href="https://nas.nijholt-energy.nl:9393/IDCONS/IDCONS.html">https://nas.nijholt-energy.nl:9393/IDCONS/IDCONS.html</a></p>
<h3 class="code-line" data-line-start=186 data-line-end=187 ><a id="How_to_apply_a_quick_fix_in_the_NGINX_config_186"></a>How to apply a quick fix in the NGINX config</h3>
<ol>
<li class="has-line-data" data-line-start="187" data-line-end="188">ssh to machine running is, e.g. ssh <a href="mailto:sysadmin@acc.idcons.nl">sysadmin@acc.idcons.nl</a> / see pwsafe for password</li>
<li class="has-line-data" data-line-start="188" data-line-end="189">find the appropriate docker container using docker ps -&gt; e.g. 6ce4ae557202</li>
<li class="has-line-data" data-line-start="189" data-line-end="190">edit the file on the host: sudo vi /opt/nginx/config/ssl.idcons.conf</li>
<li class="has-line-data" data-line-start="190" data-line-end="192">restart the container: docker restart 6ce4ae557202</li>
</ol>
<h3 class="code-line" data-line-start=192 data-line-end=193 ><a id="How_to_copy_data_from_ACC_or_PROD_to_your_local_laptop_192"></a>How to copy data from ACC or PROD to your local laptop</h3>
<p class="has-line-data" data-line-start="193" data-line-end="196">For prod you can use the script docker/axon-restore/restore_from_prod.sh and follow instructions.<br>
Or you can use docker/axon-restore/restore_backup.sh if you don’t want a fresh backup from prod.<br>
Below are the manual instructions:</p>
<ol>
<li class="has-line-data" data-line-start="196" data-line-end="202">
<p class="has-line-data" data-line-start="196" data-line-end="197">Get a backup from /opt/backup/axondb/ on any database node</p>
<ul>
<li class="has-line-data" data-line-start="197" data-line-end="198">see pwsafe (get on VPN first!) for url and use sysadmin account</li>
<li class="has-line-data" data-line-start="198" data-line-end="199">e.g. ssh <a href="mailto:sysadmin@acc-db03.idcons.nl">sysadmin@acc-db03.idcons.nl</a> / &lt;see pwsafe&gt;</li>
<li class="has-line-data" data-line-start="199" data-line-end="202">file: /opt/backup/axondb/acc-db03-idcons/axondb-backup-latest.tgz<br>
so: scp <a href="mailto:sysadmin@acc-db03.idcons.nl">sysadmin@acc-db03.idcons.nl</a>:/opt/backup/axondb/acc-db03-idcons/axondb-backup-latest.tgz .</li>
</ul>
</li>
<li class="has-line-data" data-line-start="202" data-line-end="209">
<p class="has-line-data" data-line-start="202" data-line-end="208">Create temp dir unzip and untar this in what is known as the “restore location”:<br>
/Users/wilco/tmp<br>
Mv *tgz to tmp<br>
Gunzip<br>
Untar<br>
=&gt; e.g. restore_location: /Users/wilco/tmp</p>
</li>
<li class="has-line-data" data-line-start="209" data-line-end="217">
<p class="has-line-data" data-line-start="209" data-line-end="216">Prepare local environment by deleting all data<br>
Stop app<br>
Stop dockers<br>
docker system prune<br>
docker volume prune<br>
Clean Mongo DB if needed (delete all Collections) e.g. by running:<br>
mongo &lt; dropAllCollectionOfLocalMongoDB.js</p>
</li>
<li class="has-line-data" data-line-start="217" data-line-end="223">
<p class="has-line-data" data-line-start="217" data-line-end="222">Copy the data from the restore location to your Docker instance running AxonDB<br>
<code>docker run -i --rm -v docker_axondb:/events -v /Users/wilco/tmp:/restore busybox cp -R /restore/backup/events /</code><br>
Verification:<br>
<code>docker run -i --rm -v docker_axondb:/events -v /Users/wilco/tmp:/restore busybox ls -la /events/default</code><br>
Should show “event” and “snapshot” files</p>
</li>
<li class="has-line-data" data-line-start="223" data-line-end="226">
<p class="has-line-data" data-line-start="223" data-line-end="225">Start dockers and wait until your AxonDB is avail. Verify it has events<br>
<a href="http://localhost:8023">http://localhost:8023</a> -&gt; should show a considerable number of events e.g. 224032 events</p>
</li>
<li class="has-line-data" data-line-start="226" data-line-end="228">
<p class="has-line-data" data-line-start="226" data-line-end="227">Start application</p>
</li>
<li class="has-line-data" data-line-start="228" data-line-end="232">
<p class="has-line-data" data-line-start="228" data-line-end="231">Replay (see also above):<br>
Use the script docker/replay.sh or execute manually:<br>
curl -XPOST -H “Content-Type: application/json” <a href="http://localhost:8080/eventprocessing/replayall">http://localhost:8080/eventprocessing/replayall</a> -d &lt;replay-token&gt;</p>
</li>
<li class="has-line-data" data-line-start="232" data-line-end="235">
<p class="has-line-data" data-line-start="232" data-line-end="234">Track replay progress (see also above):<br>
curl -XPOST -H “Content-Type: application/json” <a href="http://localhost:8080/eventprocessing/replayprogress">http://localhost:8080/eventprocessing/replayprogress</a> -d &lt;replay-token&gt;</p>
</li>
<li class="has-line-data" data-line-start="235" data-line-end="238">
<p class="has-line-data" data-line-start="235" data-line-end="237">Gather statistics on events per user (NB since last restart only as it is an in mem only):<br>
curl -XPOST -H “Content-Type: application/json” <a href="http://localhost:8080/eventprocessing/eventstats">http://localhost:8080/eventprocessing/eventstats</a> -d &lt;replay-token&gt;</p>
</li>
</ol>
<h3 class="code-line" data-line-start=238 data-line-end=239 ><a id="How_to_connect_to_mongodb_accprod_readwrite_238"></a>How to connect to mongodb acc/prod read/write</h3>
<ol>
<li class="has-line-data" data-line-start="239" data-line-end="240">obtain mongodb from Gitlab secrets e.g. for ACC: uri: mongodb://&lt;user&gt;:&lt;password&gt;@acc-db01.idcons.nl,<a href="http://acc-db02.idcons.nl">acc-db02.idcons.nl</a>,<a href="http://acc-db03.idcons.nl:27017/idcons?ssl=true&amp;replicaSet=idcons">acc-db03.idcons.nl:27017/idcons?ssl=true&amp;replicaSet=idcons</a></li>
<li class="has-line-data" data-line-start="240" data-line-end="241">concat the value of &lt;ACC_MANUAL_SSL_CERT&gt; and &lt;ACC_MANUAL_SSL_KEY&gt; into a single file client.pem</li>
<li class="has-line-data" data-line-start="241" data-line-end="242">put the value of &lt;ACC_MONGODB_SSL_CA_PEM&gt; in a file ca.pem</li>
<li class="has-line-data" data-line-start="242" data-line-end="243">lookup the value of the keystore password &lt;ACC_WEBAPP_KEYSTORE_PASSWORD&gt;</li>
<li class="has-line-data" data-line-start="243" data-line-end="244">connect to mongo db <code>mongo &lt;URI&gt; --ssl --sslCAFile ca.pem --sslPEMKeyFile client.pem --sslPEMKeyPassword &lt;sslPemKeyPassword&gt;</code></li>
<li class="has-line-data" data-line-start="244" data-line-end="247">when you need to drop the whole database, connect as regular user (usually ‘idcons’) like this:<br>
mongo mongodb://idcons:&lt;password&gt;@acc-db01.idcons.nl,<a href="http://acc-db02.idcons.nl">acc-db02.idcons.nl</a>,<a href="http://acc-db03.idcons.nl:27017/idcons?ssl=true">acc-db03.idcons.nl:27017/idcons?ssl=true</a> --ssl --sslCAFile ca.pem --sslPEMKeyFile crtkey.pem --sslPEMKeyPassword &lt;sslPemKeyPassword&gt; --sslAllowInvalidCertificates<br>
and use:</li>
</ol>
<blockquote>
<p class="has-line-data" data-line-start="247" data-line-end="252">use idcons<br>
Next, drop each collection like:<br>
db.trackingtokens.drop();<br>
see if your done using<br>
show collections</p>
</blockquote>
<h3 class="code-line" data-line-start=253 data-line-end=254 ><a id="How_to_connect_to_mongodb_dev_readwrite_253"></a>How to connect to mongodb dev read/write</h3>
<ol>
<li class="has-line-data" data-line-start="254" data-line-end="255">ssh tunnel to primary db node using the following command <code>ssh -L localport:hostname:remoteport hostname</code> for example for vagrant <code>ssh -L 27017:idcons-db1:27017 idcons-db1</code></li>
<li class="has-line-data" data-line-start="255" data-line-end="256">concat the certificate and key using the following command: <code>cat client.crt client.key &gt; client.pem</code></li>
<li class="has-line-data" data-line-start="256" data-line-end="258">connect to the mongo db <code>mongo localhost:27017 -u &lt;mongoUsername&gt; -p &lt;mongoPass&gt; --authenticationDatabase &lt;authDB&gt; --ssl --sslCAFile ca.cert --sslPEMKeyFile client.pem --sslPEMKeyPassword &lt;sslPemKeyPassword&gt;</code></li>
</ol>
<h3 class="code-line" data-line-start=258 data-line-end=259 ><a id="How_to_connect_to_mongodb_accprod_readwrite_with_Compass_258"></a>How to connect to mongodb acc/prod read/write with Compass</h3>
<ol>
<li class="has-line-data" data-line-start="259" data-line-end="260">SSH into a db server (i.e. <code>ssh sysadmin@acc-db03.idcons.nl</code>)</li>
<li class="has-line-data" data-line-start="260" data-line-end="265">Exec into the docker container, and retrieve the contents of <code>ca.pem</code> and <code>crtkey.pem</code> inside the /config folder and save as THREE seperate files (so split up crtkey.pem) on your local machine<pre><code class="has-line-data" data-line-start="262" data-line-end="265">docker ps -&gt; find mongo container ID/hash
docker exec -it &lt;mongo container hash&gt; /bin/bash
cd config
</code></pre>
</li>
<li class="has-line-data" data-line-start="265" data-line-end="268">Close the previous SSH connection make a new tunneled one (the Compass built-in tunnel does not seem to work):<pre><code class="has-line-data" data-line-start="267" data-line-end="268">ssh -L 27017:localhost:27017 sysadmin@acc-db03.idcons.nl
</code></pre>
</li>
<li class="has-line-data" data-line-start="268" data-line-end="283">Input the following settings in Compass:<pre><code class="has-line-data" data-line-start="270" data-line-end="283">Hostname: localhost
Port: 27017
Authentication X.509
Username: &lt;Leave empty&gt;

More Options -&gt;
Read Preference: Primary Preferred
SSL: Server and Client Validation
Certificate authority: &lt;File created from contents of ca.pem&gt;
Client certificate: &lt;File created from first part of crtkey.pem&gt;
Client Private Key &lt;File created from second part of crtkey.pem&gt;
Client Key Password &lt;Leave empty&gt;
SSH Tunnel: None
</code></pre>
</li>
<li class="has-line-data" data-line-start="283" data-line-end="285">Connect!</li>
</ol>
<h3 class="code-line" data-line-start=285 data-line-end=286 ><a id="How_to_connect_to_mongodb_accprod_readwrite_285"></a>How to connect to mongodb acc/prod read/write</h3>
<ol>
<li class="has-line-data" data-line-start="286" data-line-end="287">Obtain mongodb url</li>
<li class="has-line-data" data-line-start="287" data-line-end="288">Copy the ca.pem from the mongodb cluster configuration located at <code>/opt/mongodb-cluster/config</code> to the mongo docker image</li>
<li class="has-line-data" data-line-start="288" data-line-end="289">Create crtkey.pem file with the ACC_MANUAL_SSL_CERT &amp; ACC_MANUAL_SSL_KEY env variables.</li>
<li class="has-line-data" data-line-start="289" data-line-end="290">Bash into the mongo docker image in one of the db nodes.</li>
<li class="has-line-data" data-line-start="290" data-line-end="299">Connect to mongo db <code>mongo mongodb://&lt;user&gt;:&lt;password&gt;@&lt;URL&gt;:&lt;port&gt;/&lt;db&gt;?ssl=true --ssl --sslCAFile ca.pem --sslPEMKeyFile crtkey.pem --sslPEMKeyPassword &lt;WEBAPP_KEYSTORE_PASSWORD&gt;</code><br>
(for the values of url/ port /db / user / password / WEBAPP_KEYSTORE_PASSWORD see the secrets)<br>
So steps are:<br>
ssh <a href="mailto:sysadmin@acc-db01.idcons.nl">sysadmin@acc-db01.idcons.nl</a><br>
docker ps<br>
docker exec -ti &lt;image&gt; bash<br>
cd /opt<br>
mongo mongodb:…<br>
within mongo yiou should see PRIMARY as prompt (usually node 01). Then e.g.</li>
</ol>
<blockquote>
<p class="has-line-data" data-line-start="299" data-line-end="302">use idcons<br>
show collections<br>
db.personEntry.drop()</p>
</blockquote>
<h3 class="code-line" data-line-start=303 data-line-end=304 ><a id="How_to_replace_self_signed_certificates_For_Mongodb_nodes_connection_WebApp_to_Mongodb_connection__Manual_operations_connections_303"></a>How to replace self signed certificates (For Mongodb nodes connection, WebApp to Mongodb connection &amp; Manual operations connections)</h3>
<ol>
<li class="has-line-data" data-line-start="305" data-line-end="306">Generate and save certs for the environment using <code>deployment/ssl/selfsigned/generate_mongodb_webapp_manual_certs.sh</code></li>
<li class="has-line-data" data-line-start="306" data-line-end="307">Save MANUAL_OPS certs locally or in your password manager.</li>
<li class="has-line-data" data-line-start="307" data-line-end="308">Change &lt;env&gt;_WEBAPP_SSL_CERT, &lt;env&gt;_WEBAPP_SSL_KEY &amp; &lt;env&gt;_WEBAPP_KEYSTORE_PASSWORD env variables</li>
<li class="has-line-data" data-line-start="308" data-line-end="309">Change &lt;env&gt;_MONGODB_SSL_CERT, &lt;env&gt;_MONGODB_SSL_KEY &amp; &lt;env&gt;_MONGODB_SSL_CA_PEM env variables</li>
<li class="has-line-data" data-line-start="309" data-line-end="311">spring.data.mongodb.uri should contain ?ssl=true</li>
</ol>
<h3 class="code-line" data-line-start=311 data-line-end=312 ><a id="How_to_replace_client_facing_certificates_from_external_certificate_authority_311"></a>How to replace client facing certificates from external certificate authority</h3>
<ol>
<li class="has-line-data" data-line-start="312" data-line-end="313">Extract the certificates provided</li>
<li class="has-line-data" data-line-start="313" data-line-end="315">Replace the  &lt;env&gt;_IDCONS_SSL_CA_PEM, &lt;env&gt;_IDCONS_SSL_KEY &amp; &lt;env&gt;_IDCONS_SSL_CERT</li>
</ol>
<p class="has-line-data" data-line-start="315" data-line-end="316"><strong>As from 0540c2e9f236d0229f7b02950a3beb057ee73bfb &lt;env&gt;_IDCONS_SSL_CRTKEY_PEM is conctructed through the concatination of &lt;env&gt;_IDCONS_SSL_CERT &amp; &lt;env&gt;_IDCONS_SSL_KEY. This does not need to be in the enviorment variables anymore.</strong></p>
<h3 class="code-line" data-line-start=317 data-line-end=318 ><a id="How_to_replace_Axon_snapshot_files_317"></a>How to replace Axon snapshot files</h3>
<p class="has-line-data" data-line-start="318" data-line-end="319">We ran into trouble when serializing a snapshot for an aggregate without getters. The symptoms were:</p>
<ul>
<li class="has-line-data" data-line-start="319" data-line-end="320">when updating an entity, you get Axon Exception “IncompatibleAggregateException: Aggregate identifier must be non-null after applying an event. Make sure the aggregate identifier is initialized at the latest when handling the creation event.”.</li>
<li class="has-line-data" data-line-start="320" data-line-end="321">NOT all instances of the same entity suffer from this problem</li>
<li class="has-line-data" data-line-start="321" data-line-end="323">creating a new instance of the entity succeeds and you can happily update it too, even more than 50 updates (which is the snapshot trigger level) all succeed, unless the application is restarted (caches are cleared), and you try to update the aggregate</li>
</ul>
<p class="has-line-data" data-line-start="323" data-line-end="324">So, when somehow snapshots are corrupt or you want to start with a clean slate, and you already tested this locally, then act as follows for ACC/PROD clusters:</p>
<ul>
<li class="has-line-data" data-line-start="324" data-line-end="325">run a backup</li>
<li class="has-line-data" data-line-start="325" data-line-end="326">stop the application on the central HOST (docker stop &lt;image&gt;)</li>
<li class="has-line-data" data-line-start="326" data-line-end="327">ssh to all DB nodes as sysadmin and stop the docker instances running Axon</li>
<li class="has-line-data" data-line-start="327" data-line-end="329">when ALL those Axon dockers are stopped and you are still on the DB host, then fire<br>
<code>docker run --rm -it -v axondb-cluster_axondb-data:/data/ ubuntu /bin/bash</code></li>
<li class="has-line-data" data-line-start="329" data-line-end="330">you are now running ‘bash’ on a temporary ubuntu image which has the Axon data mounted</li>
<li class="has-line-data" data-line-start="330" data-line-end="332">on that image, go to the Axon data directory:<br>
<code>cd /data/events/default</code></li>
<li class="has-line-data" data-line-start="332" data-line-end="333">delete all *.snapshot files</li>
<li class="has-line-data" data-line-start="333" data-line-end="334"><code>exit</code> to leave the temporary docker image and return to the DB host</li>
<li class="has-line-data" data-line-start="334" data-line-end="335">repeat deletion for all Axon nodes</li>
<li class="has-line-data" data-line-start="335" data-line-end="336">when ALL Axon dockers are cleaned up this way, start them up again one by one (docker start &lt;image&gt;)</li>
<li class="has-line-data" data-line-start="336" data-line-end="337">finally start the docker image running the application</li>
<li class="has-line-data" data-line-start="337" data-line-end="338">log onto the system using a browser as usual</li>
<li class="has-line-data" data-line-start="338" data-line-end="341">VERIFY on the DB host and Axon docker image that *.snapshot files are re-created<br>
It could be that the application appears ill responsive for a while. This is due to Axon re-creating its snapshots.</li>
</ul>
<h3 class="code-line" data-line-start=341 data-line-end=342 ><a id="How_to_update_ORtools_341"></a>How to update OR-tools</h3>
<ol>
<li class="has-line-data" data-line-start="342" data-line-end="351">Java-code jar
<ol>
<li class="has-line-data" data-line-start="343" data-line-end="344">Go to github: <a href="https://github.com/google/or-tools/releases">https://github.com/google/or-tools/releases</a></li>
<li class="has-line-data" data-line-start="344" data-line-end="345">Download Ubuntu binary version of or-tools (or-tools_ubuntu-20.10_v8.1.8487.tar.gz)</li>
<li class="has-line-data" data-line-start="345" data-line-end="346">Extract</li>
<li class="has-line-data" data-line-start="346" data-line-end="347">Copy ortools-java-{version}.jar to idcons/lib</li>
<li class="has-line-data" data-line-start="347" data-line-end="348">Copy pom_local.xml to idcons/lib/ortools-pom.xml</li>
<li class="has-line-data" data-line-start="348" data-line-end="349">Edit <a href="http://install.sh">install.sh</a> and change the pointer to the new jar-file</li>
<li class="has-line-data" data-line-start="349" data-line-end="350">Run <a href="http://install.sh">install.sh</a></li>
<li class="has-line-data" data-line-start="350" data-line-end="351">Rebuild back-end: <code>mvn clean install -Dskip.unit.tests=true -pl back-end</code></li>
</ol>
</li>
<li class="has-line-data" data-line-start="351" data-line-end="355">Native linux libraries
<ol>
<li class="has-line-data" data-line-start="352" data-line-end="353">Download java_linux.tar.gz</li>
<li class="has-line-data" data-line-start="353" data-line-end="354">Extract</li>
<li class="has-line-data" data-line-start="354" data-line-end="355">Copy <a href="http://libortools.so">libortools.so</a> and <a href="http://libjniortools.so">libjniortools.so</a> from within the ortools-linux-x86-64-{version}.jar to idcons/lib/native/</li>
</ol>
</li>
<li class="has-line-data" data-line-start="355" data-line-end="359">Native windows libraries<br>
1 Download java_win.zip
<ol>
<li class="has-line-data" data-line-start="357" data-line-end="358">Extract</li>
<li class="has-line-data" data-line-start="358" data-line-end="359">Copy jniortools.dll from within the ortools-wis32-x86-64-{version}.jar to idcons/lib/native/</li>
</ol>
</li>
<li class="has-line-data" data-line-start="359" data-line-end="364">Native OSX libraries
<ol>
<li class="has-line-data" data-line-start="360" data-line-end="361">Download java_osx.zip</li>
<li class="has-line-data" data-line-start="361" data-line-end="362">Extract</li>
<li class="has-line-data" data-line-start="362" data-line-end="364">Copy libjniortools.dylib and libortools.dylib from within the ortools-darwin-{version}.jar to idcons/lib/native/</li>
</ol>
</li>
</ol>
<h3 class="code-line" data-line-start=364 data-line-end=365 ><a id="How_to_analyse_event_handling_performance_364"></a>How to analyse event handling performance</h3>
<p class="has-line-data" data-line-start="365" data-line-end="367">The CustomEventListenerLoggingInterceptor logs (INFO) the execution time of every event being handled by a listener. This information can be used to pin-point the slower event-handling logic. Below are some shell oneliners that make analysing this data easy<br>
These one-liners do assume a log-file exists containing the log-errors. In the run-configuration in IntelliJ you can configure a log-file for the application. To analyse all events it’s necessary to run a replay first.</p>
<h5 class="code-line" data-line-start=368 data-line-end=369 ><a id="execution_time_per_individual_event_handled_368"></a>execution time per individual event handled</h5>
<p class="has-line-data" data-line-start="369" data-line-end="370">Output: Linenumber, listener class name, event class name, aggregate identifier, execution time (ms) with the highest execution time on top</p>
<pre><code class="has-line-data" data-line-start="371" data-line-end="373" class="language-shell">grep -r executionTime -n logs/console.log | awk '{p=index($1, &quot;:&quot;); print substr($1, 0, p-1) &quot; &quot; $12 &quot; &quot; $15 &quot; &quot; $17 &quot; &quot; substr($21, 0, length($21)-2)}' | sort -n -k5 -r | less
</code></pre>
<h5 class="code-line" data-line-start=374 data-line-end=375 ><a id="Total_execution_time_spent_per_listener_class_and_event_class_combination_374"></a>Total execution time spent per listener class and event class combination</h5>
<p class="has-line-data" data-line-start="375" data-line-end="376">Output: Listener class name combined with event class name, summed execution time (ms) with the highest summed execution time on top</p>
<pre><code class="has-line-data" data-line-start="377" data-line-end="379" class="language-shell">grep -r executionTime -n logs/console.log | awk '{p=index($1, &quot;:&quot;); print substr($1, 0, p-1) &quot; &quot; $12 &quot; &quot; $15 &quot; &quot; $17 &quot; &quot; substr($21, 0, length($21)-2)}' | sort -n -k5 -r | awk '{a[$2 $3] += $5} END { for (i in a) {print i &quot;: &quot; a[i]}}' | sort -n -k2 -r | less
</code></pre>
