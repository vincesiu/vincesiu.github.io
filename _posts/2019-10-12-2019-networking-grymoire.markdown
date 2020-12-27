---
layout: post
title:  "Networking Grymoire"
date:   2019-10-12 10:43:51 +0000
categories: networking grymoire
---

# Networking Grymoire

Random tidbits that I need to reference every now and then. Everything is assumed linux

## DNS

### Dig

A lookup, going from name to ipv4 address

```
dig A @<dns server, preferably 8.8.8.8> <name>
```

Reverse lookup, going from ip address to name
```
# both are valid
dig -x 1.2.3.4
dig 4.3.2.1.in-addr.arpa
```

The key to look at the header sections for a better idea of what to do. For this header, we see 'ANSWER: 1'. This is good! This tells us that there is an answer 
```
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 260
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1
```

If we shoot a dig request to a non-existent dns name, we get the following. The status is 'NXDOMAIN'.
```
;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 14234
;; flags: qr rd ra; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1
```

To find the authoritative servers, shoot an SOA request (start of authority) instead of a regular A request.

### nslookup

if you want all the records for a dns name
```
nslookup -type=any www.yahoo.com
```

for a certain type of record
```
nslookup -query=ns www.yahoo.com
```

## traceroute things

### mtr

```
mtr <ip address>
```

## firewall

### ufw

// allowing a new rule
ufw allow 8080/tcp

// where are those dang rules?
sudo find / -type f -iname 'user*rules' -ipath '*ufw*'

// defaults
ufw allow ssh
ufw default deny incoming
ufw default allow outgoing
ufw enable

## ip things

### ip route

// List all routes
ip route list
// Set a new default route
ip route add default via 192.168.1.1 dev eth1
// Check what interface we use for a given destination
ip route get 8.8.8.8
