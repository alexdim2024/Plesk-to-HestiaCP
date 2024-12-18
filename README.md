# Plesk-to-HestiaCP
A Bash script designed to facilitate the migration of user accounts from the latest version of Plesk to the Hestia Control Panel. This script automates the transfer process, including account data, website files, databases, email accounts, and DNS records, ensuring a seamless and efficient migration between the two hosting platforms.

## The script should ensure the following functionalities:

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

**Plesk Password Handling:** Plesk has removed the option to extract the password from shared hosting subscriptions. Therefore, you will need to reset the password in HestiaCP, although the username will remain the same.

**Database Password Handling:** The script may encounter issues when attempting to set the same database password in HestiaCP due to differences in encryption mechanisms. Occasionally, a mismatch occurs when updating passwords to match those in the Plesk control panel.

**Email Password Handling:** New passwords must be set because the existing ones in Plesk are encrypted using methods such as CRYPT, DIGEST-MD5, SCRAM-SHA-1, SCRAM-SHA-256, and APOP. These encryption methods make it impossible to retrieve the passwords directly from the Plesk control panel.

**Addon Domains:** The script works reliably for domain names linked directly to Plesk subscriptions. However, addon domains that are not associated with a Plesk shared hosting subscription are handled differently: only the files are copied, without complete migration of other account elements. (If your domains are located outside of /home/$domain, you will need to update line 163 in the script.)

**Subdomains:** The script works reliably for domain names linked directly to Plesk subscriptions. However, addon subdomains that are not associated with a Plesk shared hosting subscription are handled differently: only the files are copied, without complete migration of other account elements. (If your subdomains are located outside of /home/$domain, you will need to update line 163 in the script.)

<h2>How to Use Our Script</h2>  

Follow the steps below to successfully migrate accounts from Plesk to HestiaCP using our script:  

## Prerequisites  
- Ensure that `rsync` is installed on your Plesk server.  

## How to Use  

### Step 1: Backup all the data
Ensure that you have backed up all your data. While the script has been tested in a production environment, we do not accept any responsibility for its use or misuse.

### Step 2: Ensure Hosting Plans Match  
Before running the migration script, ensure that the corresponding hosting plan is pre-configured in HestiaCP. The plans on both servers must match in name and specifications.  

### Example Comparison  
-------------------------------------------------
| **Plesk Server Plan** | **HestiaCP Plan**     |  
|------------------------|----------------------|  
| **Plan A**             | **Plan A**           |  
| 5GB storage            | 5GB storage          |  
| 5 domains              | 5 domains            |  
| 500 Emails             | 500 Emails           |  
| 200GB bandwidth        | 200GB bandwidth      |  
| 50 MySQL databases     | 50 MySQL databases   |  
-------------------------------------------------

### Step 3: Set Up SSH Access  

1. Generate an SSH key on the Plesk server:  
   ```bash
   ssh-keygen -t rsa -b 4096
   ```

2. Copy the SSH key to the HestiaCP server:

   ```bash
   ssh-copy-id -i ~/.ssh/id_rsa.pub root@<HestiaCP-Server-IP-Address>
   ```
   
3. Test the SSH connection between the two servers: 

   ```bash
   ssh root@<HestiaCP-Server-IP-Address>
   ```  

### Step 4: Download and Prepare the Script  
1. Download the migration script to the Plesk server.  
2. Place the script in the '/root' directory or any preferred folder.  
3. Set the appropriate execution permissions: 

   ```bash
   chmod +x /root/plesk_to_hestia
   ```  

### Step 5: Run the Migration Script  
Run the script using the following command: 

```bash
bash /root/plesk_to_hestia migrate <Domain-Name> <HestiaCP-Server-IP-Address> <Plesk-Account-Username>
```  

### Example Command  
For example, to migrate the domain `example.com` with username `example_user` to a HestiaCP server at `192.168.1.100`:  

```bash
bash /root/plesk_to_hestia migrate example.com 192.168.1.100 example_user
```  

## Notes  
- Ensure the SSH connection between the servers is working properly before running the script.  
- Verify that the target hosting plan exists in HestiaCP and matches the Plesk account plan.  

For software development or hosting services, visit us at: [https://www.web-project.co.uk/](https://www.web-project.co.uk/)

