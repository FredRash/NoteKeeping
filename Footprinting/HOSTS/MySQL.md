For attacking [SQL Databases](obsidian://open?vault=Obsidian%20Vault&file=Exploit%2FATTACKING%20COMMON%20SERVICES%2FAttacking%20SQL%20Databases)
```shell
# nmap enumartion
sudo nmap 10.129.14.128 -sV -sC -p3306 --script mysql*
# connecting
mysql -u root -h 10.129.14.132 (no password)
mysql -u root -pP4SSw0rd -h 10.129.14.128 (password)
```

|   |   |
|---|---|
|Command|Description|
|`mysql -u <user> -p<password> <IP address>`|Connect to the MySQL server. There should **not** be a space between the '-p' flag, and the password.|
|`show databases;`|Show all databases.|
|`use <database>;`|Select one of the existing databases.|
|`show tables;`|Show all available tables in the selected database.|
|`show columns from <table>;`|Show all columns in the selected database.|
|`select * from <table>;`|Show everything in the desired table.|
|`select * from <table> where <column> = "<string>";`|Search for needed `string` in the desired table.|
