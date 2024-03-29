* SNMP can be in every machine. It does not have a port! always try to test it!
* NFS in nmap scan show as bunch of ports under single service as "RPC"
* Question to ask when Footprinting:
	* What can we see?
	- What reasons can we have for seeing it?
	- What image does what we see create for us?
	- What do we gain from it?
	- How can we use it?
	- What can we not see?
	- What reasons can there be that we do not see?
	- What image results for us from what we do not see?
## Principles
|**`No.`**|**`Principle`**|
|---|---|
|1.|There is more than meets the eye. Consider all points of view.|
|2.|Distinguish between what we see and what we do not see.|
|3.|There are always ways to gain more information. Understand the target.|

## Six Layers of Methodology
|**Layer**|**Description**|**Information Categories**|
|---|---|---|
|`1. Internet Presence`|Identification of internet presence and externally accessible infrastructure.|Domains, Subdomains, vHosts, ASN, Netblocks, IP Addresses, Cloud Instances, Security Measures|
|`2. Gateway`|Identify the possible security measures to protect the company's external and internal infrastructure.|Firewalls, DMZ, IPS/IDS, EDR, Proxies, NAC, Network Segmentation, VPN, Cloudflare|
|`3. Accessible Services`|Identify accessible interfaces and services that are hosted externally or internally.|Service Type, Functionality, Configuration, Port, Version, Interface|
|`4. Processes`|Identify the internal processes, sources, and destinations associated with the services.|PID, Processed Data, Tasks, Source, Destination|
|`5. Privileges`|Identification of the internal permissions and privileges to the accessible services.|Groups, Users, Permissions, Restrictions, Environment|
|`6. OS Setup`|Identification of the internal components and systems setup.|OS Type, Patch Level, Network config, OS Environment, Configuration files, sensitive private files|

