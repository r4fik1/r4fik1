---
title: "Web Requests"
excerpt: "**Web Requests** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_web_requests/banner.png
  teaser: /assets/images/HTB_web_requests/upper.jpg
  og_image: /assets/images/HTB_web_requests/upper.jpg
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
![image-center](\assets\images\HTB_web_requests\upper.jpg)
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

## HyperText Transfer Protocol (HTTP)

>*Q. To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above.

## HTTP Requests and Responses

>*Q. What is the HTTP method used while intercepting the request? (case-sensitive)

>*Q. Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)

## HTTP Headers

>*Q. The server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.

## GET

>*Q. The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is the request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.

## POST

>*Q. Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'

## CRUD API

>*Q. First, try to update any city's name to be 'flag'. Then, delete any city. Once done, search for a city named 'flag' to get the flag.