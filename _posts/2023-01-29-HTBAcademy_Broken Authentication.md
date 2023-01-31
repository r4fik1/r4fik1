---
title: "Broken Authentication"
excerpt: "**Broken Authentication** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_looking_glass/banner.png
  teaser: /assets/images/HTB_looking_glass/auth.jpg
  og_image: /assets/images/HTB_looking_glass/auth.jpg
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
![image-center](\assets\images\HTB_looking_glass\auth.jpg)
## Module Summary
This module covers common vulnerabilities and misconfigurations regarding Authentication that could be leveraged to gain unauthorized access to a web application. Specifically, in this module, we will cover:

  - An overview of authentication methods
  - Common protection mechanisms and possible bypasses
  - Attacks against login processes
  - Attacks against credential handling

## Default Credentials

>*Q. Inspect the login page and perform a bruteforce attack. What is the valid username?



## Weak Bruteforce Protections

>*Q. Observe the web application based at subdirectory /question1/ and infer rate limiting. What is the wait time imposed after an attacker hits the limit? (round to a 10-second timeframe, e.g., 10 or 20)

>*Q. Work on webapp at URL /question2/ and try to bypass the login form using one of the method showed. What is the flag?

## Brute Forcing Usernames

>*Q. Find the valid username on the web app based at the /question1/ subdirectory. PLEASE NOTE: Use the same wordlist for all four questions.

>*Q. Find the valid username for the web application based at subdirectory /question2/.

>*Q. Find the valid account name for the web application based at subdirectory /question3/.

>*Q. Now find another way to discover the valid username for the web application based at subdirectory /question4/ .

## Brute Forcing Passwords

>*Q. Using rockyou-50.txt as password wordlist and htbuser as the username, find the policy and filter out strings that don't respect it. What is the valid password for the htbuser account?

## Predictable Reset Token

>*Q. Create a token on the web application exposed at subdirectory /question1/ using the *Create a reset token for htbuser* button. Within an interval of +-1 second a token for the htbadmin user will also be created. The algorithm used to generate both tokens is the same as the one shown when talking about the Apache OpenMeeting bug. Forge a valid token for htbadmin and login by pressing the "Check" button. What is the flag?

>*Q. Request a reset token for htbuser and find the encoding algorithm, then request a reset token for htbadmin to force a password change and forge a valid temp password to login. What is the flag?

## Guessable Answers

>*Q. Reset the htbadmin user's password by guessing one of the questions. What is the flag?

## Username Injection

>*Q. Login with the credentials "htbuser:htbuser" and abuse the reset password function to escalate to "htbadmin" user. What is the flag?

## Brute Forcing Cookies

>*Q. Tamper the session cookie for the application at subdirectory /question1/ to give yourself access as a super user. What is the flag?

>*Q. Log in to the target application and tamper the rememberme token to give yourself super user privileges. After escalating privileges, submit the flag as your answer.

## Skill Assessment - Broken Authentication

>*Q. Assess the web application and use various techniques to escalate to a privileged user and find a flag in the admin panel. Submit the contents of the flag as your answer.
