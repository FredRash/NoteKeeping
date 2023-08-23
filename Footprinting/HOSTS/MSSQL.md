For attacking [SQL Databases](obsidian://open?vault=Obsidian%20Vault&file=Exploit%2FATTACKING%20COMMON%20SERVICES%2FAttacking%20SQL%20Databases)
The same concept of [MySQL](obsidian://open?vault=Obsidian%20Vault&file=Footprinting%2FHOSTS%2FMySQL) and [TNS](obsidian://open?vault=Obsidian%20Vault&file=Footprinting%2FHOSTS%2FOracle%20TNS) 
```bash
# nmap enumartion
sudo nmap --script ms-sql-info,ms-sql-empty-password,ms-sql-xp-cmdshell,ms-sql-config,ms-sql-ntlm-info,ms-sql-tables,ms-sql-hasdbaccess,ms-sql-dac,ms-sql-dump-hashes --script-args mssql.instance-port=1433,mssql.username=sa,mssql.password=,mssql.instance-name=MSSQLSERVER -sV -p 1433 10.129.201.248

# Recon with MetaSploit
auxiliary/scanner/mssql/mssql_ping 

# Connect with mssqlclient
python3 mssqlclient.py Administrator@10.129.201.248 -windows-auth
# Using sqsh with widnows Authntication
sqsh -S <IP> -U .\\<Username> -P <Password> -D <Database>
# using normal sqsh
sqsh -S <IP> -U <Username> -P <Password> -D <Database>
```
