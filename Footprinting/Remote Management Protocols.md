# SSH
```bash
# general inforamtion 
ssh-audit 10.129.14.132

# Change Authentication Method
ssh -v cry0l1t3@10.129.14.132

# for brute force
ssh -v cry0l1t3@10.129.14.132 -o PreferredAuthentications=password
```

# Rsync
```bash
# nmap enumartion
sudo nmap -sV -p 873 127.0.0.1

# see what can be accessed
nc -nv 127.0.0.1 873

# enumarting a share file
rsync -av --list-only rsync://127.0.0.1/sharefile

# sync files to attack
rsync -av rsync://127.0.0.1/sharefile
# with ssh
rsync -av -e rsync://127.0.0.1/dev
```

# R-Services
|**Command**|**Service Daemon**|**Port**|**Transport Protocol**|**Description**|
|---|---|---|---|---|
|`rcp`|`rshd`|514|TCP|Copy a file or directory bidirectionally from the local system to the remote system (or vice versa) or from one remote system to another. It works like the `cp` command on Linux but provides `no warning to the user for overwriting existing files on a system`.|
|`rsh`|`rshd`|514|TCP|Opens a shell on a remote machine without a login procedure. Relies upon the trusted entries in the `/etc/hosts.equiv` and `.rhosts` files for validation.|
|`rexec`|`rexecd`|512|TCP|Enables a user to run shell commands on a remote machine. Requires authentication through the use of a `username` and `password` through an unencrypted network socket. Authentication is overridden by the trusted entries in the `/etc/hosts.equiv` and `.rhosts` files.|
|`rlogin`|`rlogind`|513|TCP|Enables a user to log in to a remote host over the network. It works similarly to `telnet` but can only connect to Unix-like hosts. Authentication is overridden by the trusted entries in the `/etc/hosts.equiv` and `.rhosts` files.|

```bash
# enumartion with nmap
sudo nmap -sV -p 512,513,514 10.0.17.2

# login to r-service
rlogin 10.0.17.2 -l htb-student
```

## RDP
```bash
# nmap enumartion
nmap -sV -sC 10.129.201.248 -p3389 --script rdp*

# track individual packages
nmap -sV -sC 10.129.201.248 -p3389 --packet-trace --disable-arp-ping -n

# security check
./rdp-sec-check.pl 10.129.201.248

# Initiate an RDP Session
xfreerdp /u:cry0l1t3 /p:"P455w0rd!" /v:10.129.201.248
```

## WinRM
```bash
# nmap enumartion
nmap -sV -sC 10.129.201.248 -p5985,5986 --disable-arp-ping -n

# interaction witn WinRM
evil-winrm -i 10.129.201.248 -u Cry0l1t3 -p P455w0rD!
```

## WMI
```bash
# interct with WMI
/usr/share/doc/python3-impacket/examples/wmiexec.py Cry0l1t3:"P455w0rD!"@10.129.201.248 "hostname"


```