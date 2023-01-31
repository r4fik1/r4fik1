---
title: "Web Service & API Attacks"
excerpt: "**Web Service & API Attacks** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Web_Service_&_API_Attacks/banner.png
  teaser: /assets/images/HTB_Web_Service_&_API_Attacks/upper.png
  og_image: /assets/images/HTB_Web_Service_&_API_Attacks/upper.png
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
layout: single
toc: true
---
![image-center](\assets\images\HTB_Web_Service_&_API_Attacks\upper.png)
## Module Summary

Security-related inefficiencies or misconfigurations in a web service or API can have devastating consequences that range from denial of service (DoS) and information leakage to remote code execution.

From a bug bounty hunter or web application penetration tester perspective, you must know how to assess the security of web services and APIs. That said, assessing the security of a web service or API is not a small feat. This is because web services and APIs can be affected by multiple vulnerability classes.

Worry not, though; in this module, we will provide you with a highly hands-on experience around attacking web services and APIs and the most common paths that you can take to achieve that.

Specifically, you will have the opportunity to practice manual exploitation of the following vulnerabilities against real-world web services and APIs.

  - Command Injection
  - SQL Injection
  - SSRF
  - LFI
  - XSS
  - Arbitrary File Upload
  - XXE
  - ReDOS
  - SOAP SQL Injection
  - SOAPAction Spoofing
  

## Web Services Description Language (WSDL)

>*Q. If you should think of the operation object in WSDL as a programming concept, which of the following is closer in terms of the provided functionality? Answer options (without quotation marks): "Data Structure", "Method", "Class"*

## SOAPAction Spoofing

>*Q. Exploit the SOAPAction spoofing vulnerability and submit the architecture of the web server as your answer. Answer options (without quotation marks): "x86_64", "x86"*

## Command Injection

>*Q. To execute commands featuring arguments via http://<TARGET IP>:3003/ping-server.php/system/{cmd} you may have to use ______. Answer options (without quotation marks): "Encryption", "Hashing", "URL Encoding"*

>*Q. To execute commands featuring arguments via http://<TARGET IP>:3003/ping-server.php/system/{cmd} you may have to use ______. Answer options (without quotation marks): "Encryption", "Hashing", "URL Encoding"*

## Information Disclosure (with a twist of SQLi)

>*Q. What is the username of the third user (id=3)?*

>*Q. Identify the username of the user that has a position of 736373 through SQLi. Submit it as your answer.*

## Arbitrary File Upload

>*Q. Achieve remote code execution and submit the server's hostname as your answer.*

## Local File Inclusion (LFI)

>*Q. Through the LFI vulnerability identify an existing user on the server whose name starts with "ub". Answer format: ubxxxx *

## Cross-Site Scripting

>*Q. If we URL-encoded our payload twice, would it still work? Answer format: Yes, No*

## Server-Side Request Forgery (SSRF)

>*Q. Can you leverage the SSRF vulnerability to identify port 3002 listening locally on the web server? Answer format: Yes, No*

## Regular Expression Denial of Service (ReDoS)

>*Q. There are more than one payload lengths to exploit/trigger the ReDoS vulnerability. Answer format: Yes, No*

## XML External Entity (XXE) Injection

>*Q. What URI scheme should you specify inside an entity to retrieve the content of an internal file? Answer options (without quotation marks): "http", "https", "data", "file"*

## Web Service & API Attacks - Skills Assessment

>*Q. Submit the password of the user that has a username of "admin". Answer format: FLAG{string}. Please note that the service will respond successfully only after submitting the proper SQLi payload, otherwise it will hang or throw an error.*