
**Enumerating HTTP/HTTPS**

Basic Flags 
* -T -> speed 
* -p -> ports
* -A -> scan everything: script scanning,fingerprinting, versions, os, etc...
* -sU -> scan UDP 
* -sn -> for searching ip's in a network
* --mtu -> changes the packes size to a different one(needs to be divideble by 8)
* -D RND:[number] -> create decoys of ip's
* -D [list of ip's]-> create decoys of ip's that I pick in a list
* --source -> more info on ports that can't be disabled or closed
* --randomize-host -> give a list of host to scan and then nmap will jump bitween them
* -sV -> TCP scan
* --script vuln -> scan basic vulnerabilities

Basic scan -> nmap -T4 -p- -A [IP]
Basic UDP scan -> nmap -sU -p -T4 [IP]

THOUGHT
It's more efficient to start with a basic scan without the -A flag for faster results,  then when we have ports of interest we can run another scan with thouse ports with the -A flag.

Methodology
* common ports with exploit (Other ports can be exploited but not as common then thouse) - 80, 443, 139, 445
*  Defult webpage with info about server and architecture is poor hygiene is meens there probably exploits to be found.
* Find a bed link in port 80/443 to search for information disclosure
* View the source code for commands, sources, api keys, passwords, etc...


Enumerating SMB
Try to lock for protocol version or to connect to the machine via metasploit.

For more info go to the Metasploit Notes!

smbclient - tries to connect to the file share.
Example -> smbclient -L \\\\[IP]
command for connection ->smbclient \\\\[IP]\\[sharename]


Enumerating SSH
Try  connect to the SSH even if you don't have a password. For a banner.

basic connection -> ssh [ip]
Advence connection ->  ssh [ip] -oKexAlgorithms=+diffie-helman-group-shal
Even more advenced connection ->  ssh [ip] -oKexAlgorithms=+diffie-helman-group-shal -c aes128-cbc

**Using Nmap for SMTP enumeration**
Example -> nmap -p 25 --script = 
 smtp-enum-users <target Domain/IP>
