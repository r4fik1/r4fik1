---
title: "[HTB_Academy] Broken Authentication"
excerpt: "**Broken Authentication** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_broken_authentication/banner.png
  teaser: /assets/images/HTB_broken_authentication/upper.jpg
  og_image: /assets/images/HTB_broken_authentication/upper.jpg
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
![image-center](\assets\images\HTB_broken_authentication\upper.jpg)
## Module Summary
This module covers common vulnerabilities and misconfigurations regarding Authentication that could be leveraged to gain unauthorized access to a web application. Specifically, in this module, we will cover:

  - An overview of authentication methods
  - Common protection mechanisms and possible bypasses
  - Attacks against login processes
  - Attacks against credential handling

## Default Credentials

> **Q. Inspect the login page and perform a bruteforce attack. What is the valid username?**

<div style="text-align: justify">1. If we access the target and see that it is a login page </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\1.png)

<div style="text-align: justify">2. We inspect the source code of the login page and see that the title of the login page displays some interesting information: WebAccess HMI/SCADA Software. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\2.png)

<div style="text-align: justify">3. Doing a bit of searching on the internet, we found the following page: [SCADA HMI Username/Password](https://www.192-168-1-1-ip.co/router/advantech/advantech-webaccess-browser-based-hmi-and-scada-software/11215/)
in which there are several default "usernames" and "passwords" for SCADA. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\3.png)

<div style="text-align: justify">4. A brute force attack is performed using the Burpsuite tool. To do this, we first capture the login request and send it to the Burpsuite Intruder: </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\4.png)

<div style="text-align: justify">5. In the intruder we select Cluster Bomb as Attack Type and the payload positions in the "Username" and "Password" values. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\5.png)

<div style="text-align: justify">6. In the payloads tab we enter the usernames and password from step 3, both in payload set 1 and in payload set 2 and we execute the attack. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\6.png)

<div style="text-align: justify">7. In the Burpsuite results we can see how one of the requests has a different length. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\7.png)

<div style="text-align: justify">8. If we access the answer, we see how the session has been started correctly and therefore we already have the username of the question: </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\8.png)

## Weak Bruteforce Protections

>**Q. Observe the web application based at subdirectory /question1/ and infer rate limiting. What is the wait time imposed after an attacker hits the limit? (round to a 10-second timeframe, e.g., 10 or 20)**

<div style="text-align: justify">Accedemos al target y vemos que es una pagina de login. </div><br>

<div style="text-align: justify">Como la pregunta nos pide el tiempo de espera, enviamos la peticion el intruder para realizar un proceso similar al anterior.</div><br>

En el intruder seleccionamos como Attack Type "Snyper" y como payload solamente el nombre de usuario o la password (en este ejemplo usaremos el nombre de usuario).

Introducimos como payload una seria de valores aleatorios.

Ejecutamos el ataque y vemos como la longitud de la respuesta cambia en determinado momento.

Viendo la respuesta de la primera peticion con longitud diferente, descubrimos el tiempo de espera.

>**Q. Work on webapp at URL /question2/ and try to bypass the login form using one of the method showed. What is the flag?**

## Brute Forcing Usernames

>**Q. Find the valid username on the web app based at the /question1/ subdirectory. PLEASE NOTE: Use the same wordlist for all four questions.**

>**Q. Find the valid username for the web application based at subdirectory /question2/.**

>**Q. Find the valid account name for the web application based at subdirectory /question3/.**

>**Q. Now find another way to discover the valid username for the web application based at subdirectory /question4/.**

## Brute Forcing Passwords

>**Q. Using rockyou-50.txt as password wordlist and htbuser as the username, find the policy and filter out strings that don't respect it. What is the valid password for the htbuser account?**

## Predictable Reset Token

>**Q. Create a token on the web application exposed at subdirectory /question1/ using the *Create a reset token for htbuser* button. Within an interval of +-1 second a token for the htbadmin user will also be created. The algorithm used to generate both tokens is the same as the one shown when talking about the Apache OpenMeeting bug. Forge a valid token for htbadmin and login by pressing the "Check" button. What is the flag?**

>**Q. Request a reset token for htbuser and find the encoding algorithm, then request a reset token for htbadmin to force a password change and forge a valid temp password to login. What is the flag?**

## Guessable Answers

>**Q. Reset the htbadmin user's password by guessing one of the questions. What is the flag?**

## Username Injection

>**Q. Login with the credentials "htbuser:htbuser" and abuse the reset password function to escalate to "htbadmin" user. What is the flag?**

## Brute Forcing Cookies

>**Q. Tamper the session cookie for the application at subdirectory /question1/ to give yourself access as a super user. What is the flag?**

>**Q. Log in to the target application and tamper the rememberme token to give yourself super user privileges. After escalating privileges, submit the flag as your answer.**

## Skill Assessment - Broken Authentication

>**Q. Assess the web application and use various techniques to escalate to a privileged user and find a flag in the admin panel. Submit the contents of the flag as your answer.**