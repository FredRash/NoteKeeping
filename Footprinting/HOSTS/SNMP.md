```bash
query the OIDs with their information
# brute force
snmpwalk -v2c -c public 10.129.14.128
# using wordlist
onesixtyone -c /opt/useful/SecLists/Discovery/SNMP/snmp.txt 10.129.14.128
# brute-force the individual OIDs and enumerate the information behind them
braa <community string>@<IP>:.1.3.6.*
braa public@10.129.14.128:.1.3.6.*
```
