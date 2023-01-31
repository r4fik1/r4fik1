---
title: "Login Brute Forcing"
excerpt: "**Login Brute Forcing** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Login_Brute_Forcing/banner.png
  teaser: /assets/images/HTB_Login_Brute_Forcing/upper.png
  og_image: /assets/images/HTB_Login_Brute_Forcing/upper.png
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
![image-center](\assets\images\HTB_looking_glass\upper.png)
## Module Summary
A critical area of web enumeration is looking for users who use weak or common passwords and attempt to guess their passwords through brute force. Though brute-forcing is always a last resort, gaining access through brute force is still very common, as most users tend to use weak or common passwords.

In the Login Brute Forcing module, you will learn how to brute force for users who use common or weak passwords and use their credentials to log in.

You will learn the following topics:

  - Brute forcing basic HTTP authentication
  - Brute forcing website login forms
  - Creating personalized wordlists based on personal details
  - Brute-forcing service logins, like FTP, SSH, and others

## Default Passwords

>*Q. Using the technique you learned in this section, try attacking the IP shown above. What are the credentials used?

## Username Brute Force

>*Q. Try running the same exercise on the question from the previous section, to learn how to brute force for users.

## Login Form Attacks

>*Q. Using what you learned in this section, try attacking the '/login.php' page to identify the password for the 'admin' user. Once you login, you should find a flag. Submit the flag as the answer.

## Service Authentication Brute Forcing

>*Q. Using what you learned in this section, try to brute force the SSH login of the user "b.gates" in the target server shown above. Then try to SSH into the server. You should find a flag in the home dir. What is the content of the flag?

>*Q. Using what you learned in this section, try to brute force the SSH login of the user "b.gates" in the target server shown above. Then try to SSH into the server. You should find a flag in the home dir. What is the content of the flag?

## Skills Assessment - Website

>*Q. When you try to access the IP shown above, you will not have authorization to access it. Brute force the authentication and retrieve the flag.

>*Q. Once you access the login page, you are tasked to brute force your way into this page as well. What is the flag hidden inside?

## Skills Assessment - Service Login

>*Q. As you now have the name of an employee, try to gather basic information about them, and generate a custom password wordlist that meets the password policy. Also use 'usernameGenerator' to generate potential usernames for the employee. Finally, try to brute force the SSH server shown above to get the flag.

>*Q. Once you are in, you should find that another user exists in server. Try to brute force their login, and get their flag.