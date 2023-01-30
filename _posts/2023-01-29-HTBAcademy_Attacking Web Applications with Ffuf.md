---
title: "Attacking Web Applications with Ffuf"
excerpt: "**Attacking Web Applications with Ffuf** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_attacking_web_applications_with_ffuf/banner.png
  teaser: /assets/images/HTB_attacking_web_applications_with_ffuf/upper.png
  og_image: /assets/images/HTB_attacking_web_applications_with_ffuf/upper.png
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
---
![image-center](\assets\images\HTB_looking_glass\upper.png)
## Module Summary
This module introduces key fundamentals that must be mastered to be successful in information security. Understanding web requests is essential for understanding how web applications work, which is necessary before attempting to attack or secure any web application. This makes this module the very first step in web application penetration testing.

This module will deliver these concepts through two main tools: cURL and the Browser DevTools. These tools are among the essential tools in any web penetration tester's arsenal, and this module will start you on the path to mastering them.

In addition to the above, this module will cover:

  - An overview of the HyperText Transfer Protocol (HTTP)
  - An overview of the Hypertext Transfer Protocol Secure (HTTPS)
  - HTTP requests and responses and their headers
  - HTTP methods and response codes
  - Common HTTP methods such as GET, POST, PUT, and DELETE
  - Interacting with APIs


## Directory Fuzzing

>*Q. In addition to the directory we found above, there is another directory that can be found. What is it?

## Page Fuzzing

>*Q. Try to use what you learned in this section to fuzz the '/blog' directory and find all pages. One of them should contain a flag. What is the flag?

## Recursive Fuzzing

>*Q. Try to repeat what you learned so far to find more files/directories. One of them should give you a flag. What is the content of the flag?

## Sub-domain Fuzzing

>*Q. HackTheBox has an online Swag Shop. Try running a sub-domain fuzzing test on 'hackthebox.eu' to find it. What is the full domain of it?

## Filtering Results

>*Q. Try running a VHost fuzzing scan on 'academy.htb', and see what other VHosts you get. What other VHosts did you get?

## Parameter Fuzzing - GET

>*Q. Using what you learned in this section, run a parameter fuzzing scan on this page. what is the parameter accepted by this webpage?

## Value Fuzzing

>*Q. Try to create the 'ids.txt' wordlist, identify the accepted value with a fuzzing scan, and then use it in a 'POST' request with 'curl' to collect the flag. What is the content of the flag?

## Skills Assessment - Web

>*Q. Run a sub-domain/vhost fuzzing scan on '*.academy.htb' for the IP shown above. What are all the sub-domains you can identify? (Only write the sub-domain name)

>*Q. Before you run your page fuzzing scan, you should first run an extension fuzzing scan. What are the different extensions accepted by the domains?

>*Q. One of the pages you will identify should say 'You don't have access!'. What is the full page URL?

>*Q. In the page from the previous question, you should be able to find multiple parameters that are accepted by the page. What are they?

>*Q. Try fuzzing the parameters you identified for working values. One of them should return a flag. What is the content of the flag?