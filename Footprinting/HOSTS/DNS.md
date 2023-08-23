For attacking [DNS](obsidian://open?vault=Obsidian%20Vault&file=Exploit%2FATTACKING%20COMMON%20SERVICES%2FAttacking%20DNS)
```bash 
# DNS root server
The root servers of the DNS are responsible for the top-level domains (`TLD`). As the last instance, they are only requested if the name server does not respond. Thus, a root server is a central interface between users and content on the Internet, as it links domain and IP address. The Internet Corporation for Assigned Names and Numbers (`ICANN`) coordinates thework of the root name servers. There are `13` such root servers around the globe.

# Authoritative Nameserver
Authoritative name servers hold authority for a particular zone. They only answer queries from their area of responsibility, and their information is binding. If an authoritative name server cannot answer a clients query, the root name server takes over at that point.

# Non-authoritative Nameserver
Non-authoritative name servers are not responsible for a particular DNS zone. Instead, they collect information on specific DNS zones themselves, which is done using recursive or iterative DNS querying.

# Caching DNS Server
Caching DNS servers cache information from other name servers for a specified period. The authoritative name server determines the duration of this storage.

# Forwarding Server
Forwarding servers perform only one function: they forward DNS queries to another DNS server.

# Resolver
Resolvers are not authoritative DNS servers but perform name resolution locally in the computer or router.
```

```shell
dig ns inlanefreight.htb @10.129.14.128 (NS query)
dig soa www.inlanefreight.com(soa query)
dig any inlanefreight.htb @10.129.14.128 (ANY query)
dig axfr inlanefreight.htb @10.129.14.128 (AXFR zone transfer query)
dig axfr internal.inlanefreight.htb @10.129.14.128 (same but internal)

# Bruteforce sub-domains :
for sub in $(cat /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt);do dig $sub.inlanefreight.htb @10.129.14.128 | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done

dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt inlanefreight.htb
```