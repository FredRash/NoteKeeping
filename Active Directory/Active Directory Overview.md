What is AC?
* Directory service developed by Microsoft to manage Windows domain networks
* Stores info related tp Objects, such as Computers, Users, Printers, etc.
	* Think about it as a phone book for windows
* Authenticates using Kerberos tickets.
	* Non-windows devices, such as Linux machines, firewalls, etc. can also authenticate to AC via RADIUS or LDAP

Why AC?
* AC is the most commonly used identity management service in the world
	* 95% of Fortune 1000 companies implement the service in their networks
* Can be exploited without ever attacking patchable exploit.
	* Instead, we abuse features, trusts, components, and more.

Physical AC Components
* Domain Controllers are servers with the AD DS server role installed that has specifically been promoted to a domain controller
	* Host a copy of the AD DS directory store
	* Provide authentication and authorization services
	* Replicate updates to other domain controllers in the domain and forest
	* Allow administrative access to manger user accounts and network resources
* AD DS data store contains the database files and processes that store and manage directory info for users, services, and apps
	* Consists of the Ntds.dit file
	* Is stored by default in the %SystemRoot%\NTDS folder on all domain controllers
	* Is accessible only through the domain controller processes and protocols

Logical AD Components
* AD DS Schema
	* Defines every type of object that can be stored in the directory
	* Enforces rules regarding object creation and configuration
* Domains  are used to group and manage objects in an organization
	* An administrative boundary for applying policies to groups of objects
	* A replication boundary for replicating data between domain controllers
	* An authentication and authorization boundary provides a way to limit the scope of access to resources
* Domain Trees is a hierarchy of domains in AD DS
	* Share a contiguous namespace with the parent domain 
	* Can have additional child domains
	* By default create a two-way transitive trust with other domains
* Forests is a collection of one or more domains trees
	* Share common schema
	* share a common configuration 
	* share a common global catalog to enable searching
	* Enable trusts between all domains in the forest
	* Share the Enterprise Admins and Schema Admins groups
*  Organization Units (Ous) are Directory Containers that can contain users, groups. computers, and other Ous
	* Represent your organization hierarchically and logically
	* Manage a collection of objects in a consistent way
	* Delegate permissions to administer groups of objects
	* Apply policies
* Trusts provide a mechanism for users to gain access to resources in another domain
	* All domains in a forest trust all other domains in the forest 
	* Trust can extend outside the forest
*  
