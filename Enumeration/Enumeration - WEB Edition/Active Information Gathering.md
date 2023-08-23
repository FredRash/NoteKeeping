# Active Domain Enumeration

Zone transfers : [https://hackertarget.com/zone-transfer/](https://hackertarget.com/zone-transfer/)

```bash
nslookup -type=NS zonetransfer.me
nslookup -type=any -query=AXFR zonetransfer.me nsztm1.digi.ninja
```

Gobuster :

```bash
export TARGET="facebook.com"
export NS="d.ns.facebook.com"
export WORDLIST="numbers.txt"
gobuster dns -q -r "${NS}" -d "${TARGET}" -w "${WORDLIST}" -p ./patterns.txt -o "gobuster_${TARGET}.txt"
```

# Virtual Hosts

```bash
curl -s http://192.168.10.10 -H "Host: randomtarget.com"

cat ./vhosts | while read vhost;do echo "\n********\nFUZZING: ${vhost}\n********";curl -s -I http://192.168.10.10 -H "HOST: ${vhost}.randomtarget.com" | grep "Content-Length: ";done

Example :
curl -s http://192.168.10.10 -H "Host: dev-admin.randomtarget.com"

ffuf -w ./vhosts -u http://192.168.10.10 -H "HOST: FUZZ.randomtarget.com" -fs 612
```

# Crawling

```bash
ffuf -recursion -recursion-depth 1 -u http://192.168.10.10/FUZZ -w /opt/useful/SecLists/Discovery/Web-Content/raft-small-directories-lowercase.txt
```