
```bash
# Certificate transparency.
curl -s https://crt.sh/\?q\=<target-domain>\&output\=json | jq .

# Company Hosted Servers
for i in $(cat subdomainlist);do host $i | grep "has address" | grep subdomain| cut -d" " -f4 >> ip-addresses.txt;done
# Scan each IP address in a list using Shodan.
for i in $(cat ip-addresses.txt);do shodan host $i;done

# for finding info about cload services
https://buckets.grayhatwarfare.com/
```
