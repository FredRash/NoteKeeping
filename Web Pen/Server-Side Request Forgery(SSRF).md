What is SSRF?
This is a Vulnerabilty class that occurs whan an app is fetching a remote resource without first validating the user suppkied URL.

Types of SSRF
* Regular / In band - when we send a request, the app will respons with the content
* Blind / Out-of-Band - when we send a request, the respons won't show us.

How to find SSRF?
Black Box Testing(No Info  about the terget)
* Identify all any request parameters tht contain hostnames, IP, addresses or full URLs
* For each request parameter, modify its value to specify an alternative resource and observe how the app responds
	*  If a defense is in place, attempt to circumvent it using known techniques
* For each request parameter modify its value to a server on the internet that you control(NGROK) and monitor the server for incoming requests
	* If no incoming connections are recived, monitor the time taken for the application to respond

White-Box Testing
* Review source code and identify all request parameters that accept URLs
	* This could be done by combining both black-box and white-box testing perspective
* Determine what URL parser is being used and if it can be bypassed. Similarly determine what additional defenses are put in place that can be bypassed
	* Artical Name - A New Era of SSRF - Exploiting URL Parser in Trending Programming Languages by Orange Tsai
* Test any potential SSRF vulnerabilitys

How to Exploit SSRF?
Reguler / In-Band SSRF
* If the app allows for user-supplied arbitrary URLs, try the following attacks:
	* Determine if a port number can be specified
	* If successful, attempt to port-scan the internal network using burp Intruder
	* Attempt to connect to other services on the loopback address
	* Obfuscating blocked strings using URL encoding or case variation.
* If the app does not allow for arbitrary user-supploed URls, try to bypass defenses using the following techniques
	* Use different encoding schemes
		* decimal-encoded version of 127.0.0.1 is 2130706433
		* 127.1 resolves to 127.0.0.1
		* Octal representation of 127.0.0.1 is 017700000001
	* Register a domain name tht resolves to internal IP address (DNS Rebinding), You can use `spoofed.burpcollaborator.net` for this purpose.
	* Use your own server that redirects to an internl IP address(HTTP Redirection)
* The URL specification contains a number of features that are liable to be overlooked when implementing ad hoc parsing and validation of URLs:
	-  You can embed credentials in a URL before the hostname, using the `@` character. For example:`https://expected-host:fakepassword@evil-host`
	-   You can use the `#` character to indicate a URL fragment. For example:`https://evil-host#expected-host`
	-  You can leverage the DNS naming hierarchy to place required input into a fully-qualified DNS name that you control. For example:  `https://expected-host.evil-host`
	-  You can URL-encode characters to confuse the URL-parsing code. This is particularly useful if the code that implements the filter handles URL-encoded characters differently than the code that performs the back-end HTTP request. Note that you can also try [double-encoding](https://portswigger.net/web-security/essential-skills/obfuscating-attacks-using-encodings#obfuscation-via-double-url-encoding) characters; some servers recursively URL-decode the input they receive, which can lead to further discrepancies.
	-  You can use combinations of these techniques together.
* It is sometimes possible to circumvent any kind of filter-based defenses by exploiting an open redirection vulnerability.

Blind / Out-of-Band SSRF
* If the app is vulnerable to blind SSRF, try to exploit the vulnerability using the following techniques:
	* Attemp to trigger an HTTP request to an external system you control and monitor the system for network interactions from the vulnerable server
		* Can be done using Burp Collaborator/ngrok
	* If defenses are put in place, use the techniques mentioned above to obfuscate the external malicious domain
	* Once you've proved that the app is vulnerable to blind SSRF, you need to determine what your end goal is(Show example | Impact)

Things to keep in mind
* If an IP is pressent in the url try to scan the internal IP(192.168.1.0 - 192.168.1.255) range for finding more pages.
* When trying to bypass black-list, play with the first part of the URL, always try to double encode it.
* Map The fucking Website!!! Every link every fucking page! and try to find redirects to bypass some restrictions!
