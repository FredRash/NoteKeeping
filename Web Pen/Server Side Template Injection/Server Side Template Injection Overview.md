What is server-side template injection?
Server-side template injection is when an attacker is able to use native template syntax to inject a malicious payload into a template, which is then executed server-side.
 As the name suggests, server-side template injection payloads are delivered and evaluated server-side, potentially making them much more dangerous than a typical client-side template injection.

How do server-side template injection vulnerabilities arise?
Server-side template injection vulnerabilities arise when user input is concatenated into templates rather than being passed in as data.
The classic example is an email that greets each user by their name, such as the following extract from a Twig template:
`$output = $twig->render("Dear {first_name},", array("first_name" => $user.first_name) );`
This is not vulnerable to server-side template injection because the user's first name is merely passed into the template as data.

Constructing a server-side template injection attack
Identifying server-side template injection vulnerabilities and crafting a successful attack typically involves the following high-level process.

Who to find SSTI Vulnerabilities
Server-side template injection vulnerabilities often go unnoticed not because they are complex but because they are only really apparent to auditors who are explicitly looking for them. If you are able to detect that a vulnerability is present, it can be surprisingly easy to exploit it. This is especially true in unsandboxed environments.
 * The simplest initial approach is to try fuzzing the template by injecting a sequence of special characters commonly used in template expressions, such as `${{<%[%'"}}%\`.
 * Plaintext context, Most template languages allow you to freely input content either by using HTML tags directly or by using the template's native syntax, which will be rendered to HTML on the back-end before the HTTP response is sent. For example, consider a template that contains the following vulnerable code:
	`render('Hello ' + username)`
	During auditing, we might test for server-side template injection by requesting a URL such as:
	`http://vulnerable-website.com/?username=${7*7}`
* Code context, the vulnerability is exposed by user input being placed within a template expression. This may take the form of a user-controllable variable name being placed inside a parameter, such as:
	`greeting = getQueryParameter('greeting') engine.render("Hello {{"+greeting+"}}", data)`
	On the website, the resulting URL would be something like:
	`http://vulnerable-website.com/?greeting=data.username`

Identify
Once you have detected the template injection potential, the next step is to identify the template engine.
Simply submitting invalid syntax is often enough because the resulting error message will tell you exactly what the template engine is, and sometimes even which version. For example, the invalid expression `<%=foobar%>` triggers the following response from the Ruby-based ERB engine:
You'll need to manually test different language-specific payloads and study how they are interpreted by the template engine.
A common way of doing this is to inject arbitrary mathematical operations using syntax from different template engines. You can then observe whether they are successfully evaluated. To help with this process, you can use a decision tree similar to the following:![[Pasted image 20230529100348.png]]
You should be aware that the same payload can sometimes return a successful response in more than one template language. For example, the payload `{{7*'7'}}` returns `49` in Twig and `7777777` in Jinja2. Therefore, it is important not to jump to conclusions based on a single successful response.
