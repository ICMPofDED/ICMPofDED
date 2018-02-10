Hey, this is my write-up of **Mirai**. 
I'm fairly new to hacking, but I'm writing this blog mainly to get better and to more effectivly internalize the lessons I learn along the way. 

I have already hit a few other boxes, but I'm circling around back to Mirai because it is an older box, so this means it will probably be my first post on my new blog. 
So let's begin. 

I started out by using nmap on the IP (which was `10.10.10.48` at the time). However, I was trying something new out...the `--script=default` so let's see how it goes and if it works out for me. I'm writing this as I go.

Here's the result of the NMAP Default script: 
>└──╼ $nmap --script=default 10.10.10.48

> Starting Nmap 7.60 ( https://nmap.org ) at 2018-01-16 13:50 MST
> Nmap scan report for 10.10.10.48
> Host is up (0.47s latency).
> Not shown: 997 closed ports
> PORT   STATE SERVICE
> 22/tcp open  ssh
> | ssh-hostkey: 
> |   1024 aa:ef:5c:e0:8e:86:97:82:47:ff:4a:e5:40:18:90:c5 (DSA)
> |   2048 e8:c1:9d:c5:43:ab:fe:61:23:3b:d7:e4:af:9b:74:18 (RSA)
> |   256 b6:a0:78:38:d0:c8:10:94:8b:44:b2:ea:a0:17:42:2b (ECDSA)
> |_  256 4d:68:40:f7:20:c4:e5:52:80:7a:44:38:b8:a2:a7:52 (EdDSA)
> 53/tcp open  domain
> | dns-nsid: 
> |_  bind.version: dnsmasq-2.76
> 80/tcp open  http
> |_http-title: Site doesn't have a title (text/html; charset=UTF-8).

> Nmap done: 1 IP address (1 host up) scanned in 46.55 seconds

Ok, so quite a bit less information than normal, but we have a few things to check out right off the bat. Says there is a website with no title. DNS server and SSH. 
Well, I learned about another script I want to try as well before we continue. The Nmap Vulners script. However, looks like the host is down now. Perhaps someone is issuing a reset.




Ok, it didn't want to come back up so I was the one who had to issue a reset. 
Anyway...back to business. 



> └──╼ $nmap -sV --script vulners 10.10.10.48

> Starting Nmap 7.60 ( https://nmap.org ) at 2018-01-16 14:05 MST
> Nmap scan report for 10.10.10.48
> Host is up (0.47s latency).
> Not shown: 997 closed ports
> PORT   STATE SERVICE VERSION
> 22/tcp open  ssh     OpenSSH 6.7p1 Debian 5+deb8u3 (protocol 2.0)
> | vulners: 
> |   cpe:/a:openbsd:openssh:6.7p1: 
> | 	CVE-2016-8858		7.8		https://vulners.com/cve/CVE-2016-8858
> | 	CVE-2017-15906		5.0		https://vulners.com/cve/CVE-2017-15906
> | 	CVE-2016-0778		4.6		https://vulners.com/cve/CVE-2016-0778
> |_	CVE-2016-0777		4.0		https://vulners.com/cve/CVE-2016-0777
> 53/tcp open  domain  dnsmasq 2.76
> 80/tcp open  http    lighttpd 1.4.35
> |_http-server-header: lighttpd/1.4.35
> | vulners: 
> |   cpe:/a:lighttpd:lighttpd:1.4.35: 
> |_	CVE-2015-3200		5.0		https://vulners.com/cve/CVE-2015-3200
> Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel

> Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
> Nmap done: 1 IP address (1 host up) scanned in 43.83 seconds
