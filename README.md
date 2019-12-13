<h1 id="introduction">Introduction</h1>
<p><strong>Bitdefender Advanced Threat Intelligence</strong> is a  security service that enables security professionals to make more informed decisions by providing rea-ltime threat knowledge that can be easily integrated in their existing technology stack.  The solution delivers up-to-date,  contextual intelligence on URLs, IPs, domains, certificates, files, Command and Control servers and Advanced Persistent Threats to Security Operation Centers (SOCs), Managed Security Service Providers (MSSPs), Managed Detection &amp; Response (MDR) companies, IT security and investigation consultancies and large enterprises that need to block ingenious threats.</p>
<p>Bitdefender offers the following feeds as part of its offering:</p>
<ul>
<li><strong>APT-IPs-feed</strong> - <em>Feed of IPs associated with Advanced Persistent Threats</em></li>
<li><strong>APT-filehashes-feed</strong> - <em>Feed of file hashes associated with Advanced Persistent Threats</em></li>
<li><strong>CNC-IPs-feed</strong> - <em>Feed of IPs associated with command-and-control servers</em></li>
<li><strong>Phishing domains</strong> – <em>Feed with domain addresses that are known to be associated to phishing attacks</em></li>
<li><strong>Malware domains</strong> - <em>Feed with domain addresses that are known to be associated with malware</em></li>
</ul>
<p>This document describes how to integrate the Bitdefender Advanced Threat Intelligence service with the Threat Connect platform. Once the integration is succesful, the IOCs provided by Bitdefender Advanced Threat Intelligence service will be visible in the Threat Connect platform and ready for usage.</p>
<h1 id="app-installation">App installation</h1>
<h2 id="requirements">Requirements</h2>
<p>Before proceeding with the installation, please ensure the following items are already available:</p>
<ul>
<li>Access to ThreatConnect instance</li>
<li>At least one ThreatConnect API user (See <a href="https://kb.threatconnect.com/customer/en/portal/articles/2188549-creating-user-accounts">Creating User Accounts</a>)</li>
<li>Bitdefender Authentication Token . This is  provided by Bitdefender and it is used for authentication when connecting to Bitdefender Advanced Threat Intelligence services</li>
</ul>
<h2 id="installation">Installation</h2>
<p>Bitdefender Advanced Threat  Intelligence app for ThreatConnect is available on Github at: <a href="https://github.com/ThreatConnect-Inc/threatconnect-jobs/tree/master/apps/Bitdefender-Advanced%20Threat%20Intelligence">Github Link</a>. Download the app package (represented by the file with the <em>tcx</em> extension and install it in your instance.</p>
<blockquote>
<p>The steps required to install the app are outlined in the<br>
ThreatConnect System   Administration Guide (Install an App and Feed<br>
Deployer). <code>need link here</code>  Additionally, for more information you can contact your<br>
ThreatConnect Customer Success   Engineer</p>
</blockquote>
<h2 id="attributes-configuration">Attributes configuration</h2>
<h2 id="threatconnect-job-configuration">ThreatConnect Job Configuration</h2>
<blockquote>
<p><strong>Note:</strong> This step is not required for users who use Feed Deployer as it is automatically performed by the Feed Deployer Wizard</p>
</blockquote>
<p>The ThreatConnect Platform provides the ability for customers to schedule applications as jobs, specifically known as Job apps, that can<br>
be run at configured intervals. Bitdefender has developed a Job app for ThreatConnect customers by the name of Bitdefender Threat Intelligence that handles the complete process of downloading and ingesting the threat feed into the ThreatConnect Platform. In<br>
order to configure the Bitdefender job, follow the steps mentioned below:</p>
<ol>
<li>In your ThreatConnect console, navigate to the gear-icon on the top menu bar. From the drop-down menu, click on <strong>Org Settings</strong></li>
<li>Select the <strong>Apps</strong> tab , then click on the small <code>+</code> icon to add a new job</li>
<li>Enter a name for the <strong>Job</strong> name (e.g. <em>Bitdefender Daily download</em>). From the <strong>Run Program</strong> drop-down list select <strong>Bitdefender Threat Intelligence</strong> . Press <strong>Next</strong> to proceed to the next configuration screen</li>
</ol>
<blockquote>
<p><strong>Note:</strong> If you cannot see <strong>Bitdefender Threat Intelligence</strong> listed as an option, double check the App Installation step above or  contact your Customer Success Engineer</p>
</blockquote>
<ol start="4">
<li>In the next screen configure the Job parameters as follows:
<ul>
<li><strong>Bitdefeder API key</strong> : The auth token that was provided by your Bitdefender representative. If you do not have an API key, send an email to <a href="mailto:oem-sales@bitdefender.com">oem-sales@bitdefender.com</a></li>
<li><strong>Feed Type</strong> : choose the feeds for which you want data to be downloaded. The feed description can be found in the previous section - <em><strong>Introduction</strong></em></li>
<li><strong>Hash type</strong> : for each file indicators, specify the hash type you want to be added. Currently for each file indicator, MD5, SHA1 and SHA256 are available as hash types. If there is a need to have multiple hashes available for each file indicator, recreate a new job and specify a different hash value</li>
<li><strong>Threat Rating</strong> : modify the default <em>Threat Rating</em> assigned by Threat Connect</li>
<li><strong>Confidence level</strong> : modify the <em>Confidence</em> score assigned to imported indicators</li>
<li><strong>Log level</strong> : specify the Job log level. Useful when debugging the job execution</li>
<li><strong>Threat Connect Owner</strong> : select Bitdefender as the owner of imported data.</li>
</ul>
</li>
<li>Press <strong>Next</strong> to move to the next screen where options regarding job schedule can be configured:</li>
</ol>
<blockquote>
<p><strong>Note:</strong> For Confidence level, we recommend leaving a value of 100 due to the low rate of false-positive it is expected to be returned by the  Bitdefender Threat Intelligence feeds</p>
</blockquote>
<blockquote>
<p><strong>Note</strong>: Bitdefender recommends configuring the job to run on a 1h interval to ensure that the latest data is fed in the Threat Connect platform</p>
</blockquote>
<ol start="7">
<li>Finally, press <strong>Next</strong> to configure <strong>Notifications</strong> about job execution</li>
<li>Press <strong>Save</strong> to store the job in the ThreatConnect platform</li>
</ol>
<p>The new job created should be listed in the <strong>Jobs</strong> list table. The job will not run until it is marked as active.</p>
<blockquote>
<p>To activate the job, move the slider in the right direction.</p>
</blockquote>
<blockquote>
<p><strong>Note</strong>: Data will  start flowing in the Threat Connect platform either when the scheduled time is met or when a manual trigger is performed. To trigger manually the</p>
</blockquote>
<h2 id="indicator-deprecation-configuration">Indicator deprecation configuration</h2>
<p>From time to time, Bitdefender retires indicators in its threat feed that it estimates are, no longer malicious and pose any significant threat.</p>
<p>These indicators previously ingested into the ThreatConnect Platform should also be deleted accordingly to avoid false-positives.  ThreatConnect provides the ability for users to configure an indicator deprecation policy to allow ThreatConnect indicators to drop in   confidence rating if their confidence rating is not being maintained and updated. Once the indicator rating reaches a minimum value (i.e.<br>
0%), it can either be set to inactive or delete.</p>
<p>To configure an indicator deprecation policy depending upon the type of your ThreatConnect instance, please refer to the detailed knowledge-base article from ThreatConnect: CONFIGURING INDICATOR CONFIDENCE<br>
DEPRECATION (See sections Configuring Indicator Confidence Deprecation for an Organization and Configuring Indicator Confidence Deprecation for a Community or Source)</p>
<p>The recommended indicator deprecation rule settings for Bitdefender threat feed are as follows:</p>
<ul>
<li><strong>Action at Minimum</strong> selected to be <strong>Delete</strong> so that indicators are deleted as soon as they reach minimum confidence</li>
<li><strong>Percentage</strong> checkbox checked which means that indicator confidence will be dropped as a percent of its previous<br>
value</li>
<li><strong>Confidence</strong> amount set to 100 so that 100% of an indicator’s confidence is dropped</li>
<li><strong>Interval</strong> value set to 1 day which is the period after which the confidence <em>emphasized text</em>will be dropped</li>
<li><strong>Recurring</strong> checkbox also selected so that deprecation is performed on a recurring basis</li>
</ul>
<p>In simple words the recommended deprecation rule can be stated as, "<em>After every day, drop the confidence of each indicator by   100% of its previous value and when any indicator’s confidence reaches the minimum value, delete it from ThreatConnect"</em></p>
<h1 id="viewing-and-filtering-the-data">Viewing and filtering the data</h1>
<p>To view the data, click on <strong>Browse</strong> button located in the top menu of ThreatConnect console. From here, there are two options: either filter by selecting a specific <strong>Indicator</strong> or by searching for a specific indicator.</p>
<p>Each indicator imported from Bitdefender feeds will have a custom attributed named <b>Bitdefender Threat Type</b> whose value will be set according to the table below.
  

<table>
<thead>
<tr>
<th>Feed name</th>
<th>Indicator type</th>
<th>Bitdefender Threat Type</th>
</tr>
</thead>
<tbody>
<tr>
<td>APT File IP</td>
<td>Address</td>
<td>apt-ip</td>
</tr>
<tr>
<td>APT File feed</td>
<td>File</td>
<td>APT file hash</td>
</tr>
<tr>
<td>C&amp;C IP</td>
<td>Address</td>
<td>c2-ip</td>
</tr>
<tr>
<td>Phishing Domains</td>
<td>Host</td>
<td>Phishing domains</td>
</tr>
<tr>
<td>Malware Domains</td>
<td>Host</td>
<td>Malware domains</td>
</tr>
</tbody>
</table>
