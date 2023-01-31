---
title: "SQLMap Essentials"
excerpt: "**SQLMap Essentials** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_SQLMap_Essentials/banner.png
  teaser: /assets/images/HTB_SQLMap_Essentials/upper.jpg
  og_image: /assets/images/HTB_SQLMap_Essentials/upper.jpg
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
![image-center](\assets\images\HTB_SQLMap_Essentials\upper.jpg)
## Module Summary
  
Most web applications these days are connected to a database at the backend that stores various types of data the web page needs to display, from user information to front end content.

It is very common for such web applications to improperly implement calls to the database, making it possible for an attacker to manipulate the HTTP requests sent to the server to trick the database into showing more data than the developers intended. This type of attack is called a SQL Injection (SQLi).

SQLMap is an automated tool specializing in automating SQL injection discovery and exploitation, making it very trivial for pentesters to discover and exploit SQL injection vulnerabilities.

In the SQLMap Essentials module, you will learn the basics of using SQLMap to discover various types of SQL injection vulnerabilities, all the way to advanced database enumeration and retrieval of interesting data.

In this module, we will cover:

  - Overview and installation of SQLMap
  - Different types of SQL Injection attacks supported by SQLMap, and where to use each
  - Understanding the various output of SQLMap, to properly guide your attacks
  - Attacking specific parts of a web application with the use of HTTP requests
  - Dealing with various types of errors that we may be faced with when using SQLMap
  - Using various SQLMap options to tune attacks to our specific needs
  - Enumerating full databases and extracting the content of their tables, columns, and rows
  - Advanced database enumeration to find specific data
  - Finding usernames and passwords within databases and using SQLMap to crack them
  - Bypassing various types of protections that may be in place to protect the web application against SQLMap
  - Using SQLMap to read and write files to the remote server
  - Using SQLMap to execute commands on the remote server and taking complete control over it
  
## Running SQLMap on an HTTP Request

>*Q. What's the contents of table flag2? (Case #2)

>*Q. What's the contents of table flag3? (Case #3)

>*Q. What's the contents of table flag4? (Case #4)

## Attack Tuning

>*Q. What's the contents of table flag5? (Case #5)

>*Q. What's the contents of table flag6? (Case #6)

>*Q. What's the contents of table flag7? (Case #7)

## Database Enumeration

>*Q. What's the contents of table flag1 in the testdb database? (Case #1)

## Advanced Database Enumeration

>*Q. What's the name of the column containing "style" in it's name? (Case #1)

>*Q. What's the Kimberly user's password? (Case #1)

## Bypassing Web Application Protections

>*Q. What's the contents of table flag8? (Case #8)
 
>*Q. What's the contents of table flag9? (Case #9)

>*Q. What's the contents of table flag10? (Case #10)

>*Q. What's the contents of table flag11? (Case #11)

## OS Exploitation

>*Q. Try to use SQLMap to read the file "/var/www/html/flag.txt".

>*Q. Use SQLMap to get an interactive OS shell on the remote host and try to find another flag within the host.

## Skills Assessment

>*Q. What's the contents of table final_flag?