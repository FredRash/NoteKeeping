
We are locking at DNS records that could help us layout the digital structure of the network, like: mail servers, sub-domains, hidden servers...

dnsrecon - reverse lockup util.
example -> dnsrecon -r [subnet of the target] -n [ip] -d [domain name if there is't a knowen domain name use "something"]

host tool - this will use lockup for us.
basic example -> host  [domain]
Getting name servers example -> host -t(type) ns [domain]
for getting the list of all the records how can get use the host -h

dig tool - ns lockup util
Basic example -> dig [domain]
Getting name servers(secondary) -> dig -t(type) ns [domain]
Zone transfer example -> dig axfr [domain] @[primary or secondary name server]

dnsenum - does all the above automaticli
Basic example -> dnsenum [domain]
