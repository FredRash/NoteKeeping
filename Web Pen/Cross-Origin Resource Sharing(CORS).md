What is Same-Origin-Policy(Must to understand it before learning CORS)?
Same-Origin Policy is a rule that os enforced by browsers to control access to data between web application
* This does not prevent writing between web app, it prevents reading between web app
* Access is determined based on the origin

What is CORS?
Cross-Origin Resource Sharing(CORS) is a mechanism that uses HTTP headers to define origins that the browser permit loading resources. 
* CORS makes use of 2 HTTP headers
	* Access-Control-Allow-Origin
	* Access-Control-Allow-Credentials

Access-Control-Allow-Origin
Is a Header that indicates whether the response can be shared with requesting code from given origin. This header will appear in the response.
Syntax:
```
Access-Control-Allow-Origin: * -> any site can access the resources
Access-Control-Allow-Origin: <origin>
Access-Control-Allow-Origin: Null
```

Access-Control-Allow-Credentials
This is also a response header that allows cookies(or other user credentials) to be included in cross-origin requests.
Syntax:
```
Access-Control-Allow-Credentials: true
```
Note: If the server is configured with the wildcard("*") as the value of Access-Control-Allow-Origin, then the use of the credentials is not allowed.

CORS Vulnerabilities
* The Vulnerabilities arise from CORS configuration issues.
* Arise from restrictions on available options set by the Access-Control-Allow-Origin header
* The Access-Control-Allow-Origin header forces developers to use dynamic generation and if the developer implement it poorly, Vulnerabilities arise:
	*  Server-generated  Access-Control-Allow-Origin header from client-specified Origin header
	* Errors parsing Origin header
		* Granting access to all domains that end in a specific string
			* Example: bank.com
			* Bypass: maliciousbank.com
		Granting access to all domains that begin with a specific string 
	* Whitelist bull origin value

How to find CORS Vulnerabilities
Black Box Testing
* Map the App
* Test the App for dynamic generation
	* Does it reflect the user-supplied ACAO header?
	* Does it only validate on the start/end of a specifi string?
	* Does it allow the null origin?
	* Does it restirct the protocol?
	* Does it allow credentials?
* Once you have determined that a CPRS vulnerability exists, review the app functionality to deterimne how you can prove impact.

White Box Testing
* Identify the framwrok/technologies that is being used by the app
* Find out how this specific techonogy allows for CORS configuration
* Review code to identify any misconfigurations in CORS rules

Exploiting CORS Vulnerabilites
* If the app allows for credentials:
	* Server generated use supplied origin
	* Validates on the start/end of a specific string
	* Accepts the null origin
* If the app does not allow for credentials
	* what security impact does that have on the application?