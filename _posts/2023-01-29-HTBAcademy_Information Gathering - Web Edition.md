---
title: "Information Gathering - Web Edition"
excerpt: "**Information Gathering - Web Edition** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_information_gathering_web_edition/banner.png
  teaser: /assets/images/HTB_information_gathering_web_edition/upper.jpg
  og_image: /assets/images/HTB_information_gathering_web_edition/upper.jpg
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
![image-center](\assets\images\HTB_information_gathering_web_edition\upper.jpg)
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

>*Q. Perform a WHOIS lookup against the paypal.com domain. What is the registrant Internet Assigned Numbers Authority (IANA) ID number?

>*Q. What is the admin email contact for the netflix.com domain (also in-scope for the Netflix bug bounty program)?

## DNS

>*Q. Which IP address maps to paydiant.com?

>*Q. Which subdomain is returned when querying the PTR record for 173.0.87.51?

>*Q. What is the first mailserver returned when querying the MX records for paypal.com?

## Active Infrastructure Identification

>*Q. What Apache version is running on app.inlanefreight.local? (Format: 0.0.0)

>*Q. Which CMS is used on app.inlanefreight.local? (Format: word)

>*Q. Which CMS is used on app.inlanefreight.local? (Format: word)

## Active Subdomain Enumeration

>*Q. Submit the FQDN of the nameserver for the "inlanefreight.htb" domain as the answer.

>*Q. Identify how many zones exist on the target nameserver. Submit the number of found zones as the answer.

>*Q. Find and submit the contents of the TXT record as the answer.

>*Q. What is the FQDN of the IP address 10.10.34.136?

>*Q. What FQDN is assigned to the IP address 10.10.1.5? Submit the FQDN as the answer.

>*Q. Which IP address is assigned to the "us.inlanefreight.htb" subdomain. Submit the IP address as the answer.

>*Q. Submit the number of all "A" records from all zones as the answer.

## Virtual Hosts

>*Q. Enumerate the target and find a vHost that contains flag No. 1. Submit the flag value as your answer (in the format HTB{DATA}).

>*Q. Enumerate the target and find a vHost that contains flag No. 2. Submit the flag value as your answer (in the format HTB{DATA}).

>*Q. Enumerate the target and find a vHost that contains flag No. 3. Submit the flag value as your answer (in the format HTB{DATA}).

>*Q. Enumerate the target and find a vHost that contains flag No. 4. Submit the flag value as your answer (in the format HTB{DATA}).

>*Q. Find the specific vHost that starts with the letter "d" and submit the flag value as your answer (in the format HTB{DATA}).

## Information Gathering - Web - Skills Assessment

>*Q. What is the registrar IANA ID number for the githubapp.com domain?

>*Q. What is the last mailserver returned when querying the MX records for githubapp.com?

>*Q. Perform active infrastructure identification against the host https://i.imgur.com. What server name is returned for the host?

>*Q. Perform subdomain enumeration against the target githubapp.com. Which subdomain has the word 'triage' in the name?
