---
title: "[HTB] Web Attacks"
excerpt: "**Web Attacks** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Web_Attacks/banner.png
  teaser: /assets/images/HTB_Web_Attacks/upper.jpg
  og_image: /assets/images/HTB_Web_Attacks/upper.jpg
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
---
![image-center](\assets\images\HTB_Web_Attacks\upper.jpg)
## Module Summary

As web applications' popularity keeps increasing, so do the number and types of attacks that web applications are vulnerable to. Many of the most common web attacks have been covered in other web modules already. This module will cover a few other important web exploitation techniques.

The module starts by covering HTTP Verb Tampering vulnerabilities that allow attacks to manipulate HTTP requests to access restricted web pages, which may give an attacker access to sensitive resources. The second topic covered is Insecure Direct Object References (IDOR) vulnerabilities. IDORs are among the most common vulnerabilities in web applications and allow attackers to easily view and leak other user's private data due to improper access controls. Finally, the module will cover XML External Entity (XXE) Injection vulnerabilities. These recently became among the top 10 most critical web vulnerabilities, as XXE vulnerabilities may allow attackers to read local files stored on the server, gain remote code execution (RCE), or even cause a Denial of Service.

In addition to the above, the Web Attacks module will teach you the following:

  - HTTP Verb Tampering:
		* What are HTTP Verb Tampering vulnerabilities?
		* Examples of insecure configurations
		* Detecting and exploiting HTTP Verb Tampering vulnerabilities
		* Examples of secure serve configuration to prevent HTTP Verb Tampering vulnerabilities

  - IDOR:
		* What are IDOR vulnerabilities, and how do they occur
		* Examples of code vulnerable to IDOR
		* Different types of IDOR vulnerabilities
		* How to detect IDOR vulnerabilities
		* Various methods of exploiting IDOR vulnerabilities
		* Preventing IDOR vulnerabilities

  - XXE:
		* What are XXE vulnerabilities, and how do they occur
		* Examples of code vulnerable to XXE
		* Identifying and exploiting XXE vulnerabilities
		* Various XXE prevention techniques
		
## Bypassing Basic Authentication

>*Q. Try to use what you learned in this section to access the 'reset.php' page and delete all files. Once all files are deleted, you should get the flag.*

## Bypassing Security Filters
 
>*Q. To get the flag, try to bypass the command injection filter through HTTP Verb Tampering, while using the following filename: file; cp /flag.txt ./*

## Mass IDOR Enumeration

>*Q. Repeat what you learned in this section to get a list of documents of the first 20 user uid's in /documents.php, one of which should have a '.txt' file with the flag.*

## Bypassing Encoded References

>*Q. Try to download the contracts of the first 20 employee, one of which should contain the flag, which you can read with 'cat'. You can either calculate the 'contract' parameter value, or calculate the '.pdf' file name directly.*

## IDOR in Insecure APIs

>*Q. Try to read the details of the user with 'uid=5'. What is their 'uuid' value?*

## Chaining IDOR Vulnerabilities

>*Q. Try to change the admin's email to 'flag@idor.htb', and you should get the flag on the 'edit profile' page.*

## Local File Disclosure

>*Q. Try to read the content of the 'connection.php' file, and submit the value of the 'api_key' as the answer.*

## Advanced File Disclosure

>*Q. Use either method from this section to read the flag at '/flag.php'. (You may use the CDATA method at '/index.php', or the error-based method at '/error').*

## Blind Data Exfiltration

>*Q. Using Blind Data Exfiltration on the '/blind' page to read the content of '/327a6c4304ad5938eaf0efb6cc3e53dc.php' and get the flag.*

## Web Attacks - Skills Assessment

>*Q. Try to escalate your privileges and exploit different vulnerabilities to read the flag at '/flag.php'.*