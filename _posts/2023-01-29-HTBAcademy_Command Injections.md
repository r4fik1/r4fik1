---
title: "Command Injections"
excerpt: "**Command Injections** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Command_Injections/banner.png
  teaser: /assets/images/HTB_Command_Injections/upper.png
  og_image: /assets/images/HTB_Command_Injections/upper.png
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
---
![image-center](\assets\images\HTB_Command_Injections\upper.png)
## Module Summary


Command injections are among the most critical vulnerabilities in web applications, as they allow direct command execution on the hosting server, thus compromising the server and potentially the entire network. This is why it is vital to look for these types of vulnerabilities through pentesting and secure code review.

This module will teach the basics of identifying and exploiting OS command injections. It also covers techniques to bypass various filters and mitigations used to prevent the exploitation of command injections. This module covers methods for exploiting command injections on both Linux and Windows. This module will also teach how to patch command injection vulnerabilities with examples of secure code.

In addition to this, the module will teach you the following:

  - What are injections, and different types
  - Identifying code vulnerable to command injections
  - Different command injection operators we can use
  - When to use each injection operator, depending on the injection case
  - Creating a command injection payload
  - Bypassing front-end input validation and sanitization filters
  - Identifying back-end filters and security mitigations
  - Identifying which characters are blacklisted
  - Different techniques to bypass various blacklisted characters such as spaces, slashes, and semi-colons
  - Different techniques to bypass various blacklisted commands
  - Building unique obfuscation methods to bypass blacklisted commands
  - Using evasion tools to create advanced obfuscated payloads
  - How to turn vulnerable code to code that is secure against command injections



## Detection

>*Q. Try adding any of the injection operators after the ip in IP field. What did the error message say (in English)?

## Injecting Commands

>*Q. Review the HTML source code of the page to find where the front-end input validation is happening. On which line number is it?

## Other Injection Operators

>*Q. Try using the remaining three injection operators (new-line, &, |), and see how each works and how the output differs. Which of them only shows the output of the injected command?

## Identifying Filters

>*Q. Try all other injection operators to see if any of them is not blacklisted. Which of (new-line, &, |) is not blacklisted by the web application?

## Bypassing Space Filters

>*Q. Use what you learned in this section to execute the command 'ls -la'. What is the size of the 'index.php' file?

## Bypassing Other Blacklisted Characters

>*Q. Use what you learned in this section to find name of the user in the '/home' folder. What user did you find?

## Bypassing Blacklisted Commands

>*Q. Use what you learned in this section find the content of flag.txt in the home folder of the user you previously found.

## Advanced Command Obfuscation

>*Q. Find the output of the following command using one of the techniques you learned in this section: find /usr/share/ | grep root | grep mysql | tail -n 1

## Skills Assessment

>*Q. What is the content of '/flag.txt'?

