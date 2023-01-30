---
title: "Session Security"
excerpt: "**Session Security** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Session_Security/banner.png
  teaser: /assets/images/HTB_Session_Security/upper.jpg
  og_image: /assets/images/HTB_Session_Security/upper.jpg
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
---
![image-center](\assets\images\HTB_Session_Security\upper.jpg)
## Module Summary

Any inefficiencies or misconfigurations in the session-handling implementation of a web application, service, or API can have devastating consequences that range from information leakage and inadvertent user actions all the way to Account Takeover (ATO) and remote code execution.

As you can imagine, it is of paramount importance to thoroughly test the session-handling logic of a web application being assessed. That said, testing the robustness of a session-handling implementation is not a small feat. This is because chaining (seemingly unrelated) vulnerabilities is often required to successfully attack a user's session.

Worry not, though; in this module, we will provide you with a highly hands-on experience around attacking a user's session and the possible paths that you can take to achieve that.

In this module, you will have the opportunity to practice manual exploitation of the following:

  - Session Hijacking
  - Session Fixation
  - XSS (Cross-Site Scripting) <-- With a focus on user sessions
  - CSRF (Cross-Site Request Forgery)
  - Open Redirect <-- With a focus on user sessions
  
We will also discuss remediation guidance regarding the abovementioned vulnerabilities.

## Session Hijacking

>*Q. What kind of session identifier does the application employ? Answer options (without quotation marks): "URL parameter", "URL argument", "body argument", "cookie" or "proprietary solution"

## Session Fixation

>*Q. If the HttpOnly flag was set, would the application still be vulnerable to session fixation? Answer Format: Yes or No

## Obtaining Session Identifiers without User Interaction

>*Q. If xss.htb.net was an intranet application, would an attacker still be able to capture cookies via sniffing traffic if he/she got access to the company's VPN? Suppose that any user connected to the VPN can interact with xss.htb.net. Answer format: Yes or No

## Cross-Site Scripting (XSS)

>*Q. If xss.htb.net was utilizing SSL encryption, would an attacker still be able to capture cookies through XSS? Answer format: Yes or No

## Cross-Site Request Forgery

>*Q. If the update-profile request was GET-based and no anti-CSRF protections existed, would you still be able to update Ela Stienen's profile through CSRF? Answer format: Yes or No

## Cross-Site Request Forgery (GET-based)

>*Q. If csrf.htb.net was utilizing SSL encryption, would an attacker still be able to alter Julie Rogers' profile through CSRF? Answer format: Yes or No

## Cross-Site Request Forgery (POST-based)

>*Q. If csrf.htb.net was utilizing secure cookies, would an attacker still be able to leak Julie Roger's CSRF token? Answer format: Yes or No

## XSS & CSRF Chaining

>*Q. Same Origin Policy cannot prevent an attacker from changing the visibility of @goldenpeacock467's profile. Answer Format: Yes or No

## Exploiting Weak CSRF Tokens

>*Q. Our malicious page included a user-triggered event handler (onclick). To evade what kind of security measure did we do that? Answer options (without quotation marks): "Same-Origin Policy", "Popup Blockers", "XSS Filters"

## Open Redirect

>*Q. Go through the PCAP file residing in the admin's public profile and identify the flag. Answer format: FLAG{string} 

## Session Security - Skills Assessment

>*Q. Read the flag residing in the admin's public profile. Answer format: [string]

>*Q. Go through the PCAP file residing in the admin's public profile and identify the flag. Answer format: FLAG{string}