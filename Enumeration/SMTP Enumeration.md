Simple Mail Transfer Protocol.
Use netcat(nc) to connect th the SMTP server.
nc -nv [ip:SMTP port]

### Pre-Defined Commands:

-   **VRFY**: It is used to validate the user on the server.
-   **EXPN**: It is used to find the delivery address of mail aliases
-   **RCPT TO**: It points to the recipient’s address.

**Using Telnet for SMTP enumeration:**

 Telnet comes in handy in SMTP enumeration as it provides a communication channel with the host. 

 telnet <ip> <port >
	You can guess for valid user account through the following command and if you receive response code 550 it means unknown user account:
		vrfy raj@mail.lab.ignite
	
	If you received a message **code 250,251,252** which means the server has accepted the request and user account is valid.

Using Metasploit for SMTP Enumeration

Metasploit provides two SMTP auxiliary Modules i.e., smtp_enum and smtp_version. Both are used for SMTP enumeration and provide adequate information about the SMTP server. 

example smtp_enum ->
	msf > use auxiliary/scanner/smtp/smtp_enum 
	msf auxiliary(smtp_enum) set RHOSTS <IP address/target>
	msf auxiliary(smtp_enum) > set rport 25
	msf auxiliary(smtp_enum) set USER_FILE <address of file>
	msf auxiliary(smtp_enum) run

smtp_version ->

	msf > use auxiliary/scanner/smtp/smtp_version
	msf auxiliary(smtp_version) > set RHOSTS <IP address of target>
	msf auxiliary(smtp_version) > set threads 250
	msf auxiliary(smtp_version) > run