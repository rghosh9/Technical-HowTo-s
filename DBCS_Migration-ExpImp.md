## DBCS Migration to Oracle Cloud using datapump export import

### Key steps 
#### Check DBCS System

1. Make sure you have kept the generated private and public key in a safe place
2. Make sure you have kept the database password in a safe place
3. Note down the generated PDB name or your custom PDB Name
4. Make sure Oracle cloud network ports are open for database i,e 1521 and cloud monitoring
5. Make sure you have enough block storage space allocated in DBCS for export dumps and block storage files

#### Check Cloud DBCS Connectivity 
1. SSH Connectivity - ssh -i <private key> opc\@<Public IP>
2. Database connectivity with SQLPlus 

#### On-premise DBCS Checks
1. Copy the private key to a directory in on-premise DBCS
2. Securing private key files (as required by SSH) 
2a. Linux - <pre><code>chmod 400 <private key> </code></pre>
2b. Windows - Go to File properties and remove all permissions for any other users other than user using SSH
3. Copy Long cloud connection for container and the PDB databases
4. Build tnsnames alias on the tnsnames.ora file in on-premise box
5. Test SQL connectivity from on-premise to cloud DBCS databases

#### Exporting data 
2. Login into sqlplus as system and create a directory as follows 
 <pre><code>mkdir /u01/app/oracle/admin/for_cloud
 sqlplus system
Enter password: <enter the password for the SYSTEM user>
SQL> CREATE DIRECTORY dp_for_cloud AS '/u01/app/oracle/admin/for_cloud';
$ expdp system SCHEMAS=fsowner DIRECTORY=dp_for_cloud
</code></pre>
If the above do not work well, query DBA_DIRECTORIES and find the path for the DIRECTORY DATA_PUMP_DIR. Directly export from database to that path as 
<pre><code>expdp system SCHEMAS=fsowner</code></pre>

#### Copying export files directly to DBCS VM on cloud
1. Test SSH connection to cloud DBCS VM from the directory where the private key lies. (else you may need to include full path of the key)
2. Copy the zipped or unzipped datapump export file to DBMS on cloud using scp (example below)
<pre><code>$ scp –i private_key_file \
/u01/app/oracle/admin/orcl/dpdump/for_cloud/expdat.dmp \
oracle@IP_address_DBaaS_VM:/u01/app/oracle/admin/ORCL/dpdump/from_onprem</code></pre>

#### Import into DBMS 
1. Copy the file into the location pointed out by the DBMS_DATA_PUMP directory (query DBA_DIRFECTORIES logging in as system)
2. Do the following to import (alternately you may create a directory for the custom file location and do it that way as well)
<pre><code>impdp system SCHEMAS=fsowner </code></pre>
