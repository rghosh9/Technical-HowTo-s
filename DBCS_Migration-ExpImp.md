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
2. Login into sqlplus as system and create a directory as follows 
  *mkdir /u01/app/oracle/admin/orcl/dpdump/for_cloud
