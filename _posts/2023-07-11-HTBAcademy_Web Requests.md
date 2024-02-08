---
title: "[HTB_Academy] Web Requests"
excerpt: "**Web Requests** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_web_requests/banner.png
  teaser: /assets/images/HTB_web_requests/upper.jpg
  og_image: /assets/images/HTB_web_requests/upper.jpg
categories:
  - HTB-Academy
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
layout: single
toc: true
---
![image-center](\assets\images\HTB_web_requests\upper.jpg)

## Disclaimer
<img style="float: left; padding-right:10px" src="\assets\images\disclaimer.png" width="110" height="110">

<div style="text-align: justify">The following post may contain spoilers. Use it as a guide or support. It is always better to try it by yourself!</div>
<div style="text-align: justify">Enjoy :)</div>

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

>**Q. To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above.**

<div style="text-align: justify">1. A curl is executed with the IP and port that appears in the statement and as "path" "download.php". In the response you see the flag.</div><br>
![image-center](\assets\images\HTB_web_requests\Q1\1.png)

## HTTP Requests and Responses

>**Q. What is the HTTP method used while intercepting the request? (case-sensitive)**

<div style="text-align: justify">2. The curl is executed and the first line shows the HTTP method used.</div><br>
![image-center](\assets\images\HTB_web_requests\Q2\1.png)


>**Q. Send a GET request to the above server, and read the response headers to find the version of Apache running on the server, then submit it as the answer. (answer format: X.Y.ZZ)**

<div style="text-align: justify">3. In the "server" variable of the response you can see the version of Apache.</div><br>
![image-center](\assets\images\HTB_web_requests\Q2\2.png)

## HTTP Headers

>**Q. The server above loads the flag after the page is loaded. Use the Network tab in the browser devtools to see what requests are made by the page, and find the request to the flag.**

<div style="text-align: justify">4. Enter the url and access the web browser developer tools. You see a GET request with the name "flag_...".</div><br>
![image-center](\assets\images\HTB_web_requests\Q3\1.png)

<div style="text-align: justify">5. Simply click on the "response" tab to get the flag.</div><br>
![image-center](\assets\images\HTB_web_requests\Q3\2.png)

## GET

>**Q. The exercise above seems to be broken, as it returns incorrect results. Use the browser devtools to see what is the request it is sending when we search, and use cURL to search for 'flag' and obtain the flag.**

<div style="text-align: justify">6. Access the IP given by the statement. It can be seen that there is a search engine for city names on the web.</div><br>
![image-center](\assets\images\HTB_web_requests\Q4\1.png)


<div style="text-align: justify">7. Entering the city "Leeds" and accessing the request response in the developer tools of the web browser, it is seen that it is requested to execute the request using "curl".</div><br>
![image-center](\assets\images\HTB_web_requests\Q4\2.png)


<div style="text-align: justify">8. Execute the request using curl using the city "Leeds" as the parameter and the value of the token taken from the developer tools as the "Authorization" header. (This step can be done by simply copying the request as curl in the developer tools, all the headers are already included there).</div><br>
![image-center](\assets\images\HTB_web_requests\Q4\3.png)


<div style="text-align: justify">9. Performing the same request with the same header but changing the "search" parameter to the value "flag", the flag is obtained.</div><br>
![image-center](\assets\images\HTB_web_requests\Q4\4.png)

## POST

>**Q. Obtain a session cookie through a valid login, and then use the cookie with cURL to search for the flag through a JSON POST request to '/search.php'**

<div style="text-align: justify">10. Access the IP in the web browser with the developer tools open. It looks like it's a login web page.</div><br>
![image-center](\assets\images\HTB_web_requests\Q5\1.png)

<div style="text-align: justify">11. Access with the statement credentials. As in the previous question, it is a website to search for cities.</div><br>
![image-center](\assets\images\HTB_web_requests\Q5\2.png)

<div style="text-align: justify">12. Search for the city "london". In the developer tools you can see how the request uses a "JSON" with the parameter "search" and the value of the city entered "london".</div><br>
![image-center](\assets\images\HTB_web_requests\Q5\3.png)

<div style="text-align: justify">13. Create a POST curl request that has the JSON key-value pair ("search":"london") as parameters and the authentication header the PHPSESSID parameter.</div><br>
![image-center](\assets\images\HTB_web_requests\Q5\4.png)

<div style="text-align: justify">14. Execute the same curl as the previous step changing the value of the "search" parameter to "flag" and the flag is obtained.</div><br>
![image-center](\assets\images\HTB_web_requests\Q5\4.png)

## CRUD API

>**Q. First, try to update any city's name to be 'flag'. Then, delete any city. Once done, search for a city named 'flag' to get the flag.**

<div style="text-align: justify">15. Realizar una peticion curl con el path apuntantdo al valor "london". Se comprueba que la peticion a la API funciona correctamente.</div><br>
![image-center](\assets\images\HTB_web_requests\Q6\1.png)

<div style="text-align: justify">16. Perform a curl request with the path pointing to the value "leeds". It is verified that the request to the API works correctly. Two values are obtained that we can target.</div><br>
![image-center](\assets\images\HTB_web_requests\Q6\2.png)

<div style="text-align: justify">17. Using a curl request with the "PUT" method, update the value "london" to the value "flag".</div><br>
![image-center](\assets\images\HTB_web_requests\Q6\3.png)

<div style="text-align: justify">18. Perform a curl request with the "DELETE" method to delete the "leeds" value.</div><br>
![image-center](\assets\images\HTB_web_requests\Q6\4.png)

<div style="text-align: justify">19. Finally, a curl request is made pointing the path to "flag". Gets the flag in the response.</div><br>
![image-center](\assets\images\HTB_web_requests\Q6\5.png)