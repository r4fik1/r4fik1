---
title: "Using Web Proxies"
excerpt: "**Using Web Proxies** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_using_web_proxies/banner.png
  teaser: /assets/images/HTB_using_web_proxies/upper.png
  og_image: /assets/images/HTB_using_web_proxies/upper.png
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
![image-center](\assets\images\HTB_using_web_proxies\upper.png)
## Module Summary

Web applications often present an extensive attack surface. As information security professionals, it is essential to understand common attacks against a variety of frameworks and server-side languages and to be able to use tools such as intercepting web proxies effectively to analyze web applications thoroughly. This is why web application penetration testing frameworks are an essential part of any web penetration test.

Burp Suite and Zed Attack Proxy (ZAP) are powerful frameworks that can be used to test web requests on web applications, mobile apps, and thick clients. They can also be used to debug issues with web traffic from other tools and can be leveraged to perform attacks like password spraying against exposed web portals.

In this module, we will cover:

  - What are web proxies?
  - Getting starting with Burp Suite and ZAP
  - Setting up our application testing environment
  - Using Burp/ZAP to intercept and manipulate web requests
  - Using Burp/ZAP to manipulate web responses and enable disable/hidden features
  - Repeating web requests for quick testing
  - Proxying web traffic from other tools through Burp
  - Using built-in fuzzers to fuzz different endpoints and identify potential vulnerabilities
  - Using Passive/Active scanners to discover web vulnerabilities
  - Extending both tools with plugins and add-ons
  
## Intercepting Web Requests

>*Q. Try intercepting the ping request on the server shown above, and change the post data similarly to what we did in this section. Change the command to read 'flag.txt'

## Repeating Requests

>*Q. Try using request repeating to be able to quickly test commands. With that, try looking for the other flag.

## Encoding/Decoding

>*Q. The string found in the attached file has been encoded several times with various encoders. Try to use the decoding tools we discussed to decode it and get the flag.

## Proxying Tools

>*Q. Try running 'auxiliary/scanner/http/http_put' in Metasploit on any website, while routing the traffic through Burp. Once you view the requests sent, what is the last line in the request?

## Burp Intruder

>*Q. Use Burp Intruder to fuzz for '.html' files under the /admin directory, to find a file containing the flag.

## ZAP Fuzzer

>*Q. The directory we found above sets the cookie to the md5 hash of the username, as we can see the md5 cookie in the request for the (guest) user. Visit '/skills/' to get a request with a cookie, then try to use ZAP Fuzzer to fuzz the cookie for different md5 hashed usernames to get the flag. Use the "top-usernames-shortlist.txt" wordlist from Seclists.

## ZAP Scanner

>*Q. un ZAP Scanner on the target above to identify directories and potential vulnerabilities. Once you find the high-level vulnerability, try to use it to read the flag at '/flag.txt'

## Skills Assessment - Using Web Proxies

>*Q. The /lucky.php page has a button that appears to be disabled. Try to enable the button, and then click it to get the flag.

>*Q. The /admin.php page uses a cookie that has been encoded multiple times. Try to decode the cookie until you get a value with 31-characters. Submit the value as the answer.

>*Q. Once you decode the cookie, you will notice that it is only 31 characters long, which appears to be an md5 hash missing its last character. So, try to fuzz the last character of the decoded md5 cookie with all alpha-numeric characters, while encoding each request with the encoding methods you identified above. (You may use the "alphanum-case.txt" wordlist from Seclist for the payload)

>*Q. You are using the 'auxiliary/scanner/http/coldfusion_locale_traversal' tool within Metasploit, but it is not working properly for you. You decide to capture the request sent by Metasploit so you can manually verify it and repeat it. Once you capture the request, what is the 'XXXXX' directory being called in '/XXXXX/administrator/..'?