User enumeration is an important phase in penetration testing that entails identifying valid user names on a company’s network and attempting to use each of these usernames and passwords until they are able to gain unauthorized access to the system. Best practices for user enumeration are as follows:

-   Use multiple methods in identifying valid user names, such as the following:
    -   Remote command execution. 
    -   [Port scanning](https://www.geeksforgeeks.org/port-scan-in-ethical-hacking/). 
    -   Blind SQL injection 
    -   Blind LDAP injection 
    -   Blind WMI injection 
    -   Malicious web application testing 
    -   User ID from Facebook, LinkedIn, or Twitter h. Open proxy server 
    -   [Reconnaissance](https://www.geeksforgeeks.org/reconnaissance-penetration-testing/) of social media accounts 
-   Ensure that you have obtained all usernames and passwords of valid user accounts on the network.
-   In order to avoid detection, avoid using tools such as [Metasploit](https://www.geeksforgeeks.org/what-is-metasploit/), [Wireshark](https://www.geeksforgeeks.org/introduction-to-wireshark/), etc., which can be detected by some [antivirus](https://www.geeksforgeeks.org/anti-virus-its-benefits-and-drawbacks/) programs. Instead, use these tools during a penetration test to access the internal networks and test systems only.

There are some important facts about user enumeration in Ethical Hacking  are as follows:

-   Use static passwords in all important systems without any user name or email address.
-   Use it for a single system after enumerating the users.
-   Do not use it to administer or change any admin accounts on the company’s network.
-   If the system is based on Windows, you can try to get the user’s details via its credential manager service extension.
-   You can use CMD or python script to automatically enumerate the users of a system by making multiple connection attempts.
-   After gaining access, you need to verify whether the user account is valid or not. If it is valid, then your next target is to gain access to admin-level privilege using a set of tools such as Metasploit with payloads such as Meterpreter, DLL Injection, or Process Manipulation (for example Mimikatz for Windows) in order to carry out a further attack within your target network environment.