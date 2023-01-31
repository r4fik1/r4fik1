---
title: "Server-side Attacks"
excerpt: "**Server-side Attacks** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Server-side_Attacks/banner.png
  teaser: /assets/images/HTB_Server-side_Attacks/upper.png
  og_image: /assets/images/HTB_Server-side_Attacks/upper.png
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
![image-center](\assets\images\HTB_Server-side_Attacks\upper.png)
## Module Summary

When interacting with modern web applications, we need to be aware that multiple machines and components are likely involved in the process. There may be intrusion detection/prevention systems, content delivery networks for better performance, load balancers, reverse proxies, other application servers, template engines, and database servers between us and the application server. As you can imagine, the IP associated with the domain name may have nothing to do with the actual application server. When we issue HTTP requests to a target application, all the machines and components involved in the process do not simply pass requests through but also interpret them in order, for example, to apply restrictions or identify and block attacks.

At this point, we need to consider the below:

  - Do those intermediary machines and components interpret and treat the requests the same way the final application server does? If not, this could be the root cause of a security issue.
  - Do those intermediary machines and components perform (enough) validation before the user request hits the final application server? If not, this could also be the root cause of a security issue.

The attack scenarios mentioned above leverage the trust between the final application server and the intermediary machines and components. However, there are scenarios where server-side attacks can be executed against the hosting server itself without the interference of any intermediary machines and components, leveraging the trust between the server and itself. In the latter scenarios, a URL is usually passed with a hostname of 127.0.0.1 or localhost.

From a penetration tester's perspective, it is worth checking for inefficiencies in how user requests are being treated or validated from these types of intermediary machines and components or the application server itself since they can lead to severe information leakage or even remote code execution.

This module will discuss the basics of identifying and exploiting server-side bugs.

## Nginx Reverse Proxy & AJP

>*Q. Replicate the steps shown in this section to connect to the above server's "hidden" Tomcat page through the AJP proxy, then write the Tomcat version as your answer. Remember that the port you will see next to "Target:" will be the AJP proxy port. Answer format: X.X.XX

## SSRF Exploitation Example

>*Q. Replicate what you learned in this section to gain code execution on the spawned target, then look for the flag in the root directory and submit the contents as your answer.

## Blind SSRF Exploitation Example

>*Q. The target is vulnerable to blind SSRF. Leverage this blind SSRF vulnerability to interact with internal.app.local and achieve remote code execution against the internal service listening on port 5000, as you did in the previous section. Submit the kernel release number as your answer (Answer format: X.X.X-XX)

## SSI Injection Exploitation Example

>*Q. Use what you learned in this section to read the content of .htaccess.flag through SSI and submit it as your answer.

## SSTI Exploitation Example 1

>*Q. Use what you learned in this section to obtain the flag which is hidden in the environment variables. Answer format: HTB{String}

## SSTI Exploitation Example 2

>*Q. Use what you learned in this section to read the contents of flag.txt, which resides in the current working directory. Answer format: HTB{String}

## SSTI Exploitation Example 3

>*Q. Use what you learned in this section to read the contents of flag.txt, which resides in the current working directory. Answer format: HTB{String}

## Server-Side Attacks - Skills Assessment

>*Q. Read the content of 'flag.txt' through a server-side attack without registering an account and submit its content as your answer. Answer format: HTB{String}