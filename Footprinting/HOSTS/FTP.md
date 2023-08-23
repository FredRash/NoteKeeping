for attacking [FTP](obsidian://open?vault=Obsidian%20Vault&file=Exploit%2FATTACKING%20COMMON%20SERVICES%2FAttacking%20FTP) 

|**Commands**|**Description**|
|---|---|
|`connect`|Sets the remote host, and optionally the port, for file transfers.|
|`get`|Transfers a file or set of files from the remote host to the local host.|
|`put`|Transfers a file or set of files from the local host onto the remote host.|
|`quit`|Exits tftp.|
|`status`|Shows the current status of tftp, including the current transfer mode (ascii or binary), connection status, time-out value, and so on.|
|`verbose`|Turns verbose mode, which displays additional information during file transfer, on or off.|

```bash
# Anonymous Authentication
ftp 192.168.2.142
name: anonymous
password: #there is a space here

# Recursive Listing
ftp> ls -R

# Download All Available Files
wget -m --no-passive ftp://anonymous:anonymous@10.129.14.136

# Nmap enumartion
nmap -sV -p21 -sC -A 10.129.14.136

# Service Interaction
nc -nv 10.129.14.136 21
# telnet option
telnet 10.129.14.136 21

# Get SSL Certificate 
openssl s_client -connect 10.129.14.136:21 -starttls ftp
```