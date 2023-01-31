---
title: "File Inclusion"
excerpt: "**File Inclusion** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_File_Inclusion/banner.png
  teaser: /assets/images/HTB_File_Inclusion/upper.png
  og_image: /assets/images/HTB_File_Inclusion/upper.png
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
![image-center](\assets\images\HTB_File_Inclusion\upper.png)
## Module Summary

  
This module introduces the fundamentals of file inclusion vulnerabilities. Web applications often present a large attack surface, and as information security professionals, it is important to understand common attacks against a variety of frameworks and server-side languages. A successful file inclusion attack may result in sensitive data exposure (such as configuration files containing credentials) or even remote code execution.

In this module, we will cover:

  - An intro to file inclusion vulnerabilities
  - Local File Inclusion (LFI)
  - Path Traversal
  - Bypassing basic LFI restrictions
  - LFI to remote code execution (RCE)
	* RCE through PHP wrappers
	* RCE through Remote File Inclusion (RFI)
	* RCE through malicious file uploads
	* RCE through log poisoning
  - Automating LFI exploitation
  - Preventing LFI exploitation

## Local File Inclusion (LFI)

>*Q. Using the file inclusion find the name of a user on the system that starts with "b".

>*Q. Submit the contents of the flag.txt file located in the /usr/share/flags directory.

## Basic Bypasses

>*Q. The above web application employs more than one filter to avoid LFI exploitation. Try to bypass these filters to read /flag.txt

## PHP Filters

>*Q. Fuzz the web application for other php scripts, and then read one of the configuration files and submit the database password as the answer

## PHP Wrappers

>*Q. Try to gain RCE using one of the PHP wrappers and read the flag at /

## Remote File Inclusion (RFI)

>*Q. Attack the target, gain command execution by exploiting the RFI vulnerability, and then look for the flag under one of the directories in /

## LFI and File Uploads

>*Q. Use any of the techniques covered in this section to gain RCE and read the flag at /

## Log Poisoning

>*Q. Use any of the techniques covered in this section to gain RCE, then submit the output of the following command: pwd

>*Q. Try to use a different technique to gain RCE and read the flag at /

## Automated Scanning

>*Q. Fuzz the web application for exposed parameters, then try to exploit it with one of the LFI wordlists to read /flag.txt

## File Inclusion Prevention

>*Q. What is the full path to the php.ini file for Apache?

>*Q. Edit the php.ini file to block system(), then try to execute PHP Code that uses system. Read the /var/log/apache2/error.log file and fill in the blank: system() has been disabled for ________ reasons.

## Skills Assessment - File Inclusion

>*Q. Assess the web application and use a variety of techniques to gain remote code execution and find a flag in the / root directory of the file system. Submit the contents of the flag as your answer.

