What is Command Injections
* OS Command Injection is a vulnerability that consists of an attecker executing commands on the host OS via a vulnerable App.

Types of Command Injection
* In-band Command Injection, Consists an attacker executing commands on the host OS via a vulnerable application and `receving the response of the command in the app.`
* Blind Command Injection, consists of an attecker executing commands on the host OS via a vulnerable app `that does not return the output from the command within its HTTP response`

How to find Command Injection
Black Box Testing
* Identify all instances where the web application appears to be interacting with the underlying operating system
* Fuzz the app with command injection payloads
	* Shell metachracters(remember to close the command with a metacharcter or use # in the end to commnet the rest of the code):  &, &&. |, ||, ;, \n, `, $().
* For in-band command injection, analyze the response of the app to determine if it's vulnerable
* For blind command injection, you need to get creative,
	* Trigger a time delay using the ping ot sleep command.
	* Output the response of the command in the web root and retrieve the file directly using a browser
	* Open an out-of-band channel back to a server you control


White-Box Testing
* Perform a combination of black box and white-box teesting
* Map all input vectors in the app
* Review source code to determine if any of the input vectors are added parameters to functions.
* Try to Exploit!

How to Exploit The Command Injection
In-bank command Injection
* Shell metachracters(remember to close the command with a metacharcter # in the end to commnet the rest of the code):  &, &&. |, ||, ;, \n, `, $(). 
* Concatenate anthoer command, exemple - 127.0.0.1 && cat /etc/passwd &

Blind Command Inection
*  Shell metachracters(remember to close the command with a metacharcter):  &, &&. |, ||, ;, \n, `, $().
* Trigger a time delay, exemple - 127.0.01 && sleep 10 & or 127.0.01 && ping -c 127.0.0.1 &
* Output the response of the command in the web root abd retrive the file directly using a browser. Exemple - 127.0.01 & whoami > /var/www/static/whoami.txt &
* Open an out-of-band channel back to a server you control, just use the nslookup command to your server.