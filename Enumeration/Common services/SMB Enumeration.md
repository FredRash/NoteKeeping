Depending on the SMB implementation and the operating system, we will get different information using `Nmap`. Keep in mind that when targetting Windows OS, version information is usually not included as part of the Nmap scan results. Instead, Nmap will try to guess the OS version. However, we will often need other scans to identify if the target is vulnerable to a particular exploit.
nmap command for scanning SMB protocol - 
nmap [IP] -sV -sC -p139,445

The Nmap scan reveals essential information about the target:
- SMB version (Samba smbd 4.6.2)
- Hostname HTB
- Operating System is Linux based on SMB implementation

## Misconfigurations
SMB can be configured not to require authentication, which is often called a `null session`. Instead, we can log in to a system with no username or password.

#### Anonymous Authentication
If we find an SMB server that does not require a username and password or find valid credentials, we can get a list of shares, usernames, groups, permissions, policies, services, etc. Most tools that interact with SMB allow null session connectivity, including `smbclient`, `smbmap`, `rpcclient`, or `enum4linux`.

#### File Share
Using `smbclient`, we can display a list of the server's shares with the option `-L`, and using the option `-N`, we tell `smbclient` to use the null session.
smbclient -N -L //10.129.14.128

`Smbmap` is another tool that helps us enumerate network shares and access associated permissions. An advantage of `smbmap` is that it provides a list of permissions for each shared folder.
Using `smbmap` with the `-r` or `-R` (recursive) option, one can browse the directories
```shell-session
FredOsaurus@htb[/htb]$ smbmap -H 10.129.14.128

[+] IP: 10.129.14.128:445     Name: 10.129.14.128                                   
        Disk                                                    Permissions     Comment
        --                                                   ---------    -------
        ADMIN$                                                  NO ACCESS       Remote Admin
        C$                                                      NO ACCESS       Default share
        IPC$                                                    READ ONLY       IPC Service (DEVSM)
        notes                                                   READ, WRITE     CheckIT
```

```shell-session
FredOsaurus@htb[/htb]$ smbmap -H 10.129.14.128 -r notes

[+] Guest session       IP: 10.129.14.128:445    Name: 10.129.14.128                           
        Disk                                                    Permissions     Comment
        --                                                   ---------    -------
        notes                                                   READ, WRITE
        .\notes\*
        dr--r--r               0 Mon Nov  2 00:57:44 2020    .
        dr--r--r               0 Mon Nov  2 00:57:44 2020    ..
        dr--r--r               0 Mon Nov  2 00:57:44 2020    LDOUJZWBSG
        fw--w--w             116 Tue Apr 16 07:43:19 2019    note.txt
        fr--r--r               0 Fri Feb 22 07:43:28 2019    SDT65CB.tmp
        dr--r--r               0 Mon Nov  2 00:54:57 2020    TPLRNSMWHQ
        dr--r--r               0 Mon Nov  2 00:56:51 2020    WDJEQFZPNO
        dr--r--r               0 Fri Feb 22 07:44:02 2019    WindowsImageBackup
```
From the above example, the permissions are set to `READ` and `WRITE`, which one can use to upload and download the files

#### Remote Procedure Call (RPC)
We can use the `rpcclient` tool with a null session to enumerate a workstation or Domain Controller.

The `rpcclient` tool offers us many different commands to execute specific functions on the SMB server to gather information or modify server attributes like a username. We can use this [cheat sheet from the SANS Institute](https://www.willhackforsushi.com/sec504/SMB-Access-from-Linux.pdf) or review the complete list of all these functions found on the [man page](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html) of the `rpcclient`.
```shell-session
FredOsaurus@htb[/htb]$ rpcclient -U'%' 10.10.110.17

rpcclient $> enumdomusers

user:[mhope] rid:[0x641]
user:[svc-ata] rid:[0xa2b]
user:[svc-bexec] rid:[0xa2c]
user:[roleary] rid:[0xa36]
user:[smorgan] rid:[0xa37]
```
`Enum4linux` is another utility that supports null sessions, and it utilizes `nmblookup`, `net`, `rpcclient`, and `smbclient` to automate some common enumeration from SMB targets such as:
- Workgroup/Domain name
- Users information
- Operating system information
- Groups information
- Shares Folders
- Password policy information
