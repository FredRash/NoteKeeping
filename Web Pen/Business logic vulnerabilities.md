What are business logic vulnerabilities?
Business logic vulnerabilities are flaws in the design and implementation of an application that allow an attacker to elicit unintended behavior. These flaws are generally the result of failing to anticipate unusual application states that may occur and, consequently, failing to handle them safely.

How do business logic vulnerabilities arise?
Business logic vulnerabilities often arise because the design and development teams make flawed assumptions about how users will interact with the application. These bad assumptions can lead to inadequate validation of user input.

# Examples of business logic vulnerabilities

Excessive trust in client-side controls
A fundamentally flawed assumption is that users will only interact with the application via the provided web interface. This is especially dangerous because it leads to the further assumption that client-side validation will prevent users from supplying malicious input.

Failing to handle unconventional input
One aim of the application logic is to restrict user input to values that adhere to the business rules. For example, the application may be designed to accept arbitrary values of a certain data type, but the logic determines whether or not this value is acceptable from the perspective of the business.
By observing the application's response, you should try and answer the following questions:
	-   Are there any limits that are imposed on the data?
	-   What happens when you reach those limits?
	-   Is any transformation or normalization being performed on your input?

Making flawed assumptions about user behavior
One of the most common root causes of [logic vulnerabilities](https://portswigger.net/web-security/logic-flaws) is making flawed assumptions about user behavior. This can lead to a wide range of issues where developers have not considered potentially dangerous scenarios that violate these assumptions.

Trusted users won't always remain trustworthy
some applications make the mistake of assuming that, having passed these strict controls initially, the user and their data can be trusted indefinitely. This can result in relatively lax enforcement of the same controls from that point on.
If business rules and security measures are not applied consistently throughout the application, this can lead to potentially dangerous loopholes that may be exploited by an attacker.

Users won't always supply mandatory input
One misconception is that users will always supply values for mandatory input fields. Browsers may prevent ordinary users from submitting a form without a required input, but as we know, attackers can tamper with parameters in transit. This even extends to removing parameters entirely.
When probing for logic flaws, you should try removing each parameter in turn and observing what effect this has on the response. You should make sure to:
-   Only remove one parameter at a time to ensure all relevant code paths are reached.
-   Try deleting the name of the parameter as well as the value. The server will typically handle both cases differently.
-   Follow multi-stage processes through to completion. Sometimes tampering with a parameter in one step will have an effect on another step further along in the workflow.

Users won't always follow the intended sequence
Many transactions rely on predefined workflows consisting of a sequence of steps. The web interface will typically guide users through this process, taking them to the next step of the workflow each time they complete the current one. However, attackers won't necessarily adhere to this intended sequence. Failing to account for this possibility can lead to dangerous flaws that may be relatively simple to exploit.
To identify these kinds of flaws, you should use forced browsing to submit requests in an unintended sequence. For example, you might skip certain steps, access a single step more than once, return to earlier steps, and so on. Take note of how different steps are accessed. Although you often just submit a `GET` or `POST` request to a specific URL, sometimes you can access steps by submitting different sets of parameters to the same URL. As with all logic flaws, try to identify what assumptions the developers have made and where the attack surface lies. You can then look for ways of violating these assumptions.

Domain-specific flaws
In many cases, you will encounter logic flaws that are specific to the business domain or the purpose of the site.
To identify these vulnerabilities, you need to think carefully about what objectives an attacker might have and try to find different ways of achieving this using the provided functionality. This may require a certain level of domain-specific knowledge in order to understand what might be advantageous in a given context. To use a simple example, you need to understand social media to understand the benefits of forcing a large number of users to follow you.

Providing an encryption oracle
Dangerous scenarios can occur when user-controllable input is encrypted and the resulting ciphertext is then made available to the user in some way. This kind of input is sometimes known as an "encryption oracle". An attacker can use this input to encrypt arbitrary data using the correct algorithm and asymmetric key.
n this case, an attacker could potentially use the encryption oracle to generate valid, encrypted input and then pass it into other sensitive functions.