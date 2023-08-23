```bash
# Directory Fuzzing
ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ

# Extension Fuzzing
ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/indexFUZZ

# Extension Fuzzing with a flag
ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -e .php,.phps

# Page Fuzzing
ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/blog/FUZZ.php

# Recursive Fuzzing
ffuf -w wordlist.txt:FUZZ -u http://SERVER_IP:PORT/FUZZ -recursion -recursion-depth 1 -e .php -v

# Sub-domain Fuzzing
ffuf -w wordlist.txt:FUZZ -u https://FUZZ.hackthebox.eu/

# VHost Fuzzing
ffuf -w wordlist.txt:FUZZ -u http://academy.htb:PORT/ -H 'Host: FUZZ.academy.htb' -fs 

# Parameter Fuzzing - GET
ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php?FUZZ=key -fs xxx

# Parameter Fuzzing - POST
ffuf -w wordlist.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'FUZZ=key' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx

# Value Fuzzing
ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:PORT/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs xxx

```

# Wordlists
```bash
# Directory/Page Wordlist
/opt/useful/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt

# Extensions Wordlist
/opt/useful/SecLists/Discovery/Web-Content/web-extensions.txt

# Domain Wordlist
/opt/useful/SecLists/Discovery/DNS/subdomains-top1million-5000.txt

# Parameters Wordlist
/opt/useful/SecLists/Discovery/Web-Content/burp-parameter-names.txt
```