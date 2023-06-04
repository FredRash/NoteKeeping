
 What is it
  * Authentication identifies the user and confirms that they say who tey say they are
  * Session Management identifies wich subsequent HTTP requests are being made by each user(Token)
  * Acces Control determines whether the user is allowed to carry out the action that they are attempting to perform.

There are 3 types of access control
* Vertical Access Control is used to restrict access to functions not available for other users in the organization
* Horizontal Access Control enables different users to access similar resource types
* Context-Dependent Access Control restirct access to functionality and resource based on the state of the application or the user's interaction with it

Broken Access Control vulnerabilities arise when users can act outside of the intended permissions. 

There are 3 types of broken access control
* Horizontal Privilege Escalation occurs when an attacker gains access to resources belonging to another user of the same privilege level
* Vertical Privilege Escalation occurs when an attacker gains access to privileged functionality that they are not permitted to access
* Access Control Vulnerabilities in Multi-Step Processes, these types of vulnerabilities accur when access control rules are implemented on some of the steps, but ignored on others.

Exemples of Broken Access Control
* Bypassing access control checks by modifying parameters int the URL or HTML page.
* Accessing the API with missing access controls on the POST, PUT and DELETE methods
* Manipulating metadada, such as replaying or tempering with JSON Web Tokens or a cookie
* Exploiting CORS misconfiguration that allow API access from unauthorized / untrusted origins.
* Force browsing to authenticated pages as an unauthenticated user

How to find Broken Access Control Vulnerability
Black Box Testing(No Info  about the terget)
* Identify all instances where the web application appears to be interacting with the underlying operating system
* Understand how access control is implemented for easch privilege level
* Manipulate parameters that are potentaily used to make access control decision in the backend
* Automate testing using extensions like Autorize
* It's possible to try and use a non existing HTTP method to bypess Access Control
* Try to use a different HTTP method(HEAD, PUT, TRACE, OPTIONS, and DELTE)
* Find a function based on the Referer header and try to bypass it.
* If the HTTP request use's the POST method, try to change it to a GET method and transefer the body params to URL parms.

White Box Testing(Given source code and excess to the system)
 * Review the code to identify how access control is implemented in the application
 * System defaults to opem
 * Weak or missing access control checks on functions / resources
 * Missing access control rules for POST, PUT, and DELETE methods at the API level.
 * Relying solely on client-side input to perfom access control decisions
 * Validate on the App!
 * If there is a POST request, try to change it to a GET and change the body data to URL Parameters

Exploiting Access Control Vulnerabilities
* Usually just a matter of manipulated the vulnerable field / parameter

Thing to think about when searching for Broken Access Control
* An attacker might be unable to guess or predict the identifier for another user. However, the GUIDs belonging to other users might be disclosed elsewhere in the application where users are referenced, such as user messages or reviews.
* Support of the X-Original-URL and X-Rewrite-URL headers lets users override the path in the request URL using the X-Original-URL or X-Rewrite-URL HTTP request header and allows a user to access one URL but have web application return a different URL, which can bypass restrictions on higher level caches and web servers.
* In some cases, an application does detect when the user is not permitted to access the resource, and returns a redirect to the login page. However, the response containing the redirect might still include some sensitive data belonging to the targeted user, so the attack is still successful.
* suppose an application robustly enforces access control over the main administrative page at `/admin`, but for sub-pages such as `/admin/deleteUser` only inspects the `Referer` header. If the `Referer` header contains the main `/admin` URL, then the request is allowed.