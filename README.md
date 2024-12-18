# Plesk-to-HestiaCP
A Bash script designed to facilitate the migration of user accounts from the latest version of Plesk to the Hestia Control Panel. This script automates the transfer process, including account data, website files, databases, email accounts, and DNS records, ensuring a seamless and efficient migration between the two hosting platforms.

</h2>The script should ensure the following functionalities:</h2>

<li>Account Migration:</li>
Preserve the username during the migration process.

</li>Hosting Plan Migration:</li>
Transfer the hosting plan name, ensuring that the corresponding plan is pre-configured in HestiaCP before running the script.

<li>File Migration:</li>
Migrate all files associated with the hosting account.

<li>Database Migration:</li>
Transfer databases linked to the hosting account.

<li>Email Account Migration:</li>
Migrate email accounts associated with the hosting account.

<h2>Known Issues:</h2>
<li>Database Password Handling:</li>
The script may encounter issues when attempting to set the same database password in HestiaCP due to differences in encryption mechanisms. Occasionally, a mismatch occurs when updating passwords to match those in the Plesk control panel.

<li>Addon Domains:</li>
The script works reliably for domain names linked directly to Plesk subscriptions. However, addon domains that are not associated with a Plesk shared hosting subscription are handled differently: only the files are copied, without complete migration of other account elements.
