---
title: "Cross-Site Scripting (XSS)"
excerpt: "**Cross-Site Scripting (XSS)** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Cross-Site_Scripting_(XSS)/banner.png
  teaser: /assets/images/HTB_Cross-Site_Scripting_(XSS)/upper.png
  og_image: /assets/images/HTB_Cross-Site_Scripting_(XSS)/upper.png
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
---
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\upper.png)
## Module Summary

Web Application Penetration Testing is a vital part of any penetration test. It plays an essential role in identifying critical vulnerabilities that may lead to the organization's assets being compromised. Cross-Site Scripting (XSS) vulnerabilities are among the most common vulnerabilities in any web application, with studies indicating that over 80% of all web applications are vulnerable to it. An XSS vulnerability may allow an attacker to execute arbitrary JavaScript code within the target's browser, leading to various types of attacks, including compromising web admins and their web applications.

While many organizations choose to ignore XSS vulnerabilities, as it only affects end-users without having a direct ability to execute code on the back-end server, in this module, we will discuss why XSS should be taken seriously. We will discuss the three types of XSS vulnerabilities, how to identify them, and how to exploit them.

In addition to this, the Cross-Site Scripting (XSS) module will teach you the following:

  - What is an XSS vulnerability?
  - History of XSS attacks in real-life
  - What are Stored XSS, Reflected XSS, and DOM-based XSS vulnerabilities
  - Techniques to identify XSS vulnerabilities
  - Performing Defacing attacks to change the look of a website
  - Performing Phishing attacks to steal the victim's login details and to perform a phishing simulation exercise
  - Performing Session Hijacking attacks to obtain the victim's session cookie and use them to access their account
  - Front-end and Back-end steps to prevent XSS vulnerabilities and protect your web application against them
  

## Stored XSS
 
>*>*Q. To get the flag, use the same payload we used above, but change its JavaScript code to show the cookie instead of showing the url.

## Reflected XSS

>*>*Q. To get the flag, use the same payload we used above, but change its JavaScript code to show the cookie instead of showing the url.

## DOM XSS
 
>*>*Q. To get the flag, use the same payload we used above, but change its JavaScript code to show the cookie instead of showing the url.

## XSS Discovery

>*>*Q. Utilize some of the techniques mentioned in this section to identify the vulnerable input parameter found in the above server. What is the name of the vulnerable parameter? 

>*>*Q. What type of XSS was found on the above server? "name only"

## Phishing

>*>*Q. Try to find a working XSS payload for the Image URL form found at '/phishing' in the above server, and then use what you learned in this section to prepare a malicious URL that injects a malicious login form. Then visit '/phishing/send.php' to send the URL to the victim, and they will log into the malicious login form. If you did everything correctly, you should receive the victim's login credentials, which you can use to login to '/phishing/login.php' and obtain the flag.

## Session Hijacking

>*>*Q. Try to repeat what you learned in this section to identify the vulnerable input field and find a working XSS payload, and then use the 'Session Hijacking' scripts to grab the Admin's cookie and use it in 'login.php' to get the flag.

## Skills Assessment

>*>*Q. What is the value of the 'flag' cookie?