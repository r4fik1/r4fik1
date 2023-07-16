---
title: "[HTB] Information Gathering - Web Edition"
excerpt: "**Information Gathering - Web Edition** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_information_gathering_web_edition/banner.png
  teaser: /assets/images/HTB_information_gathering_web_edition/upper.jpg
  og_image: /assets/images/HTB_information_gathering_web_edition/upper.jpg
categories:
  - HTB-Academy
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Penetration Tester
  - Web
  - OWASP TOP 10
layout: single
toc: true
---
![image-center](\assets\images\HTB_information_gathering_web_edition\upper.jpg)

## Disclaimer
<img style="float: left; padding-right:10px" src="\assets\images\disclaimer.png" width="110" height="110">

<div style="text-align: justify">The following post may contain spoilers. Use it as a guide or support. It is always better to try it by yourself!</div>
<div style="text-align: justify">Enjoy :)</div>

## Resources
<img style="float: left; padding-right:10px" src="\assets\images\github.avif" width="110" height="110">
<div style="text-align: justify">All resources can be found in the following GitHub repository:</div>
[R4fik1-HTB_information_gathering_Repository](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_information_gathering_web_edition)

## Module Summary


This module will cover various techniques for passive and active information gathering from domains and web servers that we will be able to apply to almost any penetration test and most bug bounty programs.

In this module, we will cover:

  - WHOIS
  - DNS
  - (Sub)Domain Enumeration
  - Infrastructure Identification
  - Virtual Host Enumeration
  - Crawling
  
## WHOIS

>**Q. Perform a WHOIS lookup against the paypal.com domain. What is the registrant Internet Assigned Numbers Authority (IANA) ID number?**

<div style="text-align: justify">1. Run the "whois" command in terminal pointing to "paypal.com". The response is the value of the "Register IANA ID" field.</div>
```sh
whois paypal.com
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q1\1.png)

>**Q. What is the admin email contact for the tesla.com domain (also in-scope for the Tesla bug bounty program)?**

<div style="text-align: justify">2. Run "whois" filtering for the word "admin" with grep. The response is the value of the "Admin Email" field.</div>
```sh
whois tesla.com | "admin"
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q1\2.png)

## DNS

>**Q. Which IP address maps to inlanefreight.com?**

<div style="text-align: justify">3. Using "nslookup" with query "A" pointing to inlanefreight.com gets the IP address.</div>
```sh
nslookup -query=A inlanefreight.com
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q2\1.png)

>**Q. Which subdomain is returned when querying the PTR record for 173.0.87.51?**

<div style="text-align: justify">4. Using "nslookup" with the "PTR" query pointing to the IP address of the statement returns the name.</div>
```sh
nslookup -query=PTR 173.0.87.51
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q2\2.png)

>**Q. What is the first mailserver returned when querying the MX records for paypal.com?**

<div style="text-align: justify">5. Using "nslookup" with the "MX" query pointing to "paypal.com" from the statement returns the name of the mail server.</div>
```sh
nslookup -query=MX paypal.com
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q2\3.png)

## Active Infrastructure Identification

>**Q. What Apache version is running on app.inlanefreight.local? (Format: 0.0.0)**

<div style="text-align: justify">6. Simply by curling the IP of the statement, in the response parameter "Server" is the version.</div>
```sh
curl -I "http://10.129.194.206"
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q3\1.png)

>**Q. Which CMS is used on app.inlanefreight.local? (Format: word)**

<div style="text-align: justify">7. Add to the "/etc/hosts" file app.inlanefreight.local and dev.inlanefreight.local.</div>
```sh
nano /etc/hosts
```

```sh
10.129.194.206 app.inlanefreight.local dev.inlanefreight.local
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q3\2.png)

<div style="text-align: justify">8. With whatweb and the parameter "a3" the value of CMS is obtained.</div>
```sh
whatweb -a3 app.inlanefreight.local -v
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q3\3.png)

>**Q. Which CMS is used on app.inlanefreight.local? (Format: word)**

<div style="text-align: justify">9. With whatweb and the parameter "a3" the value of CMS is obtained.</div>
```sh
whatweb -a3 dev.inlanefreight.local -v
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q3\4.png)

## Active Subdomain Enumeration

>**Q. Submit the FQDN of the nameserver for the "inlanefreight.htb" domain as the answer.**

<div style="text-align: justify">10. Use nslookup with the NS type.</div>
```sh
nslookup -type=NS inlanefreight.htb 10.129.128.199
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q4\1.png)

>**Q. Identify how many zones exist on the target nameserver. Submit the number of found zones as the answer.**

<div style="text-align: justify">11. Use nslookup or dig and check the number of zones.</div>
```sh
nslookup -type=any inlanefreight.htb 10.129.128.199
```

```sh
dig ANY inlanefreight.htb @10.129.128.199
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q4\2.png)

>**Q. Find and submit the contents of the TXT record as the answer.**

<div style="text-align: justify">12. Use dig on "internal.inlanefreight.htb" with NS txt filter.</div>
```sh
dig @10.129.128.199 NS txt internal.inlanefreight.htb 
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q4\3.png)

>**Q. What is the FQDN of the IP address 10.10.34.136?**

<div style="text-align: justify">13. Using dig on "internal.inlanefreight.htb" with NS filter axfr.</div>
```sh
dig @10.129.128.199 NS axfr internal.inlanefreight.htb 
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q4\4.png)

>**Q. What FQDN is assigned to the IP address 10.10.1.5? Submit the FQDN as the answer.**

<div style="text-align: justify">14. Using dig on "internal.inlanefreight.htb" with NS filter axfr.</div>
```sh
dig @10.129.128.199 NS axfr internal.inlanefreight.htb 
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q4\5.png)

>**Q. Which IP address is assigned to the "us.inlanefreight.htb" subdomain. Submit the IP address as the answer.**

<div style="text-align: justify">15. Using dig on "us.inlanefreight.htb" with the "NS a" filter.</div>
```sh
dig @10.129.128.199 NS a us.inlanefreight.htb 
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q4\6.png)

>**Q. Submit the number of all "A" records from all zones as the answer.**

<div style="text-align: justify">16. Use dig on "internal.inlanefreight.htb" and "inlanefreight.htb" on with AXFR filter and count.</div>
```sh
dig @10.129.128.199 AXFR a inlanefreight.htb 
```

```sh
dig @10.129.128.199 AXFR a internal.inlanefreight.htb 
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q4\7.png)

## Virtual Hosts

>**Q. Enumerate the target and find a vHost that contains flag No. 1. Submit the flag value as your answer (in the format HTB{DATA}).**

<div style="text-align: justify">17. With ffuf you find the vHosts.</div>
```sh
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-lowercase-2.3-big.txt -u http://10.129.128.199 -H "HOST: FUZZ.inlanefreight.htb" -fs 10918
```

![image-center](\assets\images\HTB_information_gathering_web_edition\Q5\1.png)

<div style="text-align: justify">18. Add to the "/etc/hosts" file the previous vHosts.</div>
```sh
nano /etc/hosts
```

```sh
10.129.194.206 ***.inlanefreight.htb ***.inlanefreight.htb ***.inlanefreight.htb ***.inlanefreight.htb
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q5\1.1.png)

<div style="text-align: justify">19. Curl to the address.</div>
```sh
curl -s http://10.129.128.199 -H "Host:***.inlanefreight.htb"
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q5\2.png)

>**Q. Enumerate the target and find a vHost that contains flag No. 2. Submit the flag value as your answer (in the format HTB{DATA}).**

<div style="text-align: justify">19. Curl to the address.</div>
```sh
curl -s http://10.129.128.199 -H "Host:***.inlanefreight.htb"
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q5\3.png)


>**Q. Enumerate the target and find a vHost that contains flag No. 3. Submit the flag value as your answer (in the format HTB{DATA}).**

<div style="text-align: justify">20. Curl to the address.</div>
```sh
curl -s http://10.129.128.199 -H "Host:***.inlanefreight.htb"
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q5\4.png)

>**Q. Enumerate the target and find a vHost that contains flag No. 4. Submit the flag value as your answer (in the format HTB{DATA}).**

<div style="text-align: justify">21. Curl to the address.</div>
```sh
curl -s http://10.129.128.199 -H "Host:***.inlanefreight.htb"
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q5\5.png)

>**Q. Find the specific vHost that starts with the letter "d" and submit the flag value as your answer (in the format HTB{DATA}).**

<div style="text-align: justify">22. Curl to the address.</div>
```sh
curl -s http://10.129.128.199 -H "Host:***.inlanefreight.htb"
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q5\6.png)

## Information Gathering - Web - Skills Assessment

>**Q. What is the registrar IANA ID number for the githubapp.com domain?**

<div style="text-align: justify">23. Just use "whois" for the address.</div>
```sh
whois githubapp.com
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q6\1.png)

>**Q. What is the last mailserver returned when querying the MX records for githubapp.com?**

<div style="text-align: justify">24. Use nslookup with the MX query to githubapp.com.</div>
```sh
nslookup -query=MX githubapp.com
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q6\2.png)

>**Q. Perform active infrastructure identification against the host https://i.imgur.com. What server name is returned for the host?**

<div style="text-align: justify">25. Use whatweb with the parameter a3 to https://i.imgur.com.</div>
```sh
whatweb -a3 https://i.imgur.com
```
![image-center](\assets\images\HTB_information_gathering_web_edition\Q6\3.png)

>**Q. Perform subdomain enumeration against the target githubapp.com. Which subdomain has the word 'triage' in the name?**

<div style="text-align: justify">26. Enter githubapp.com in the web crt.sh.</div><br>
![image-center](\assets\images\HTB_information_gathering_web_edition\Q6\4.png)