---
title: "[HTB_Academy] Using Web Proxies"
excerpt: "**Using Web Proxies** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_using_web_proxies/banner.png
  teaser: /assets/images/HTB_using_web_proxies/upper.jpg
  og_image: /assets/images/HTB_using_web_proxies/upper.jpg
categories:
  - HTB-Academy
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Penetration Tester
  - Web
  - OWASP TOP 10
layout: single
toc: true
---
![image-center](\assets\images\HTB_using_web_proxies\upper.jpg)

## Disclaimer
<img style="float: left; padding-right:10px" src="\assets\images\disclaimer.png" width="110" height="110">

<div style="text-align: justify">The following post may contain spoilers. Use it as a guide or support. It is always better to try it by yourself!</div>
<div style="text-align: justify">Enjoy :)</div>

## Resources
<img style="float: left; padding-right:10px" src="\assets\images\github.avif" width="110" height="110">
<div style="text-align: justify">All resources can be found in the following GitHub repository:</div>
[R4fik1-HTB_using_web_proxies](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_using_web_proxies)

## Module Summary

Web applications often present an extensive attack surface. As information security professionals, it is essential to understand common attacks against a variety of frameworks and server-side languages and to be able to use tools such as intercepting web proxies effectively to analyze web applications thoroughly. This is why web application penetration testing frameworks are an essential part of any web penetration test.

Burp Suite and Zed Attack Proxy (ZAP) are powerful frameworks that can be used to test web requests on web applications, mobile apps, and thick clients. They can also be used to debug issues with web traffic from other tools and can be leveraged to perform attacks like password spraying against exposed web portals.

In this module, we will cover:

  - What are web proxies?
  - Getting starting with Burp Suite and ZAP
  - Setting up our application testing environment
  - Using Burp/ZAP to intercept and manipulate web requests
  - Using Burp/ZAP to manipulate web responses and enable disable/hidden features
  - Repeating web requests for quick testing
  - Proxying web traffic from other tools through Burp
  - Using built-in fuzzers to fuzz different endpoints and identify potential vulnerabilities
  - Using Passive/Active scanners to discover web vulnerabilities
  - Extending both tools with plugins and add-ons
  
## Intercepting Web Requests

>**Q. Try intercepting the ping request on the server shown above, and change the post data similarly to what we did in this section. Change the command to read 'flag.txt'**

<div style="text-align: justify">1. Access the target. It is a website that pings your IP.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q1\1.png)

<div style="text-align: justify">2. Test with the number one to send the request to BurpSuite.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q1\2.png)

<div style="text-align: justify">3. It is seen in the response how it executes the "ping" command.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q1\3.png)

<div style="text-align: justify">4. Access BurpSuite to check the request.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q1\5.png)

<div style="text-align: justify">5. And send this request to BurpSuite Repeater.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q1\5.png)

<div style="text-align: justify">6. Change the value of the "ip" parameter in the Repeater request to ";ls;". It checks that a file called "flag.txt" exists.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q1\6.png)

<div style="text-align: justify">7. Execute the request by changing the value of the "ip" parameter in the Repeater request to ";cat flag.txt;".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q1\7.png)

## Repeating Requests

>**Q. Try using request repeating to be able to quickly test commands. With that, try looking for the other flag.**

<div style="text-align: justify">8. Access the target. It is a website that pings your IP as in the previous question.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q2\1.png)

<div style="text-align: justify">9. Test with number one to send the request to BurpSuite. It is seen in the request response how it executes the "ping" command.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q2\2.png)

<div style="text-align: justify">10. Access BurpSuite to check the request. And send this request to BurpSuite Repeater.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q2\3.png)

<div style="text-align: justify">11. Cambiar el valor del parametro "ip" en la peticion del Repeater a ";ls;". El comando se ejecuta correctamente.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q2\4.png)

<div style="text-align: justify">12. Using linux commands, look for another "flag.txt" file. It is located at "../../../flag.txt".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q2\5.png)

<div style="text-align: justify">13. Run the command "cat ../../../flag.txt" to read the flag.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q2\6.png)

## Encoding/Decoding

>**Q. The string found in the attached file has been encoded several times with various encoders. Try to use the decoding tools we discussed to decode it and get the flag.**

<div style="text-align: justify">14. Download the file from HTB Academy</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q3\1.png)

<div style="text-align: justify">15. Unzip the file "encoded_flag.zip".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q3\2.png)

<div style="text-align: justify">16. Read the content of the file "encoded_flag.txt".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q3\3.png)

<div style="text-align: justify">17. Perform the following steps to decode the string. Base64 Decode -> Base64 Decode -> Base64 Decode -> Base64 Decode -> Base64 Decode -> ASCII Hex Decode -> Remove "%".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q3\4.png)

## Proxying Tools

>**Q. Try running 'auxiliary/scanner/http/http_put' in Metasploit on any website, while routing the traffic through Burp. Once you view the requests sent, what is the last line in the request?**

 <div style="text-align: justify">18. Run Metasploit and enter the parameters shown in the following image for the "auxiliary/scanner/http/http_put" tool.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q4\1.png)

<div style="text-align: justify">19. You can see the request captured in BurpSuite since the proxy "127.0.0.1:8080" has been used as a parameter in Metasploit.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q4\2.png)

## Burp Intruder

>**Q. Use Burp Intruder to fuzz for '.html' files under the /admin directory, to find a file containing the flag.**

<div style="text-align: justify">20. Access the url with the "/admin" directory from the browser to capture the request in BurpSuite.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q5\1.png)

<div style="text-align: justify">21. Send the request to the BurpSuite Intruder.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q5\2.png)

<div style="text-align: justify">22. Create a payload with the extension ".html" in the request sent to the Intruder.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q5\3.0.png)

<div style="text-align: justify">23. Load the list of payloads "common.txt".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q5\3.png)

<div style="text-align: justify">24. Add the Payload processing "Skip if matches regex".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q5\4.png)

<div style="text-align: justify">25. Activate URL-encode and click on "Start Attack".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q5\5.png)

<div style="text-align: justify">26. Sort the request list by length. There is a request with a longer length.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q5\6.png)

<div style="text-align: justify">27. See the response of the previous request and get the flag.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q5\7.png)

## ZAP Fuzzer

>**Q. The directory we found above sets the cookie to the md5 hash of the username, as we can see the md5 cookie in the request for the (guest) user. Visit '/skills/' to get a request with a cookie, then try to use ZAP Fuzzer to fuzz the cookie for different md5 hashed usernames to get the flag. Use the "top-usernames-shortlist.txt" wordlist from Seclists.**

<div style="text-align: justify">28. Access the IP of the statement in the "/skills/" directory, using the ZAP proxy to capture the request.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\1.png)

<div style="text-align: justify">29. Request captured in ZAP.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\2.png)

<div style="text-align: justify">30. Right-click and select Attack->Fuzz.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\3.png)

<div style="text-align: justify">31. Select the value of the cookie and click on Add.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\4.png)

<div style="text-align: justify">34. Click on the Payloads button once the cookie parameter has been added as Payload.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\7.png)

<div style="text-align: justify">35. Use the list "top-usernames-shortlist.txt" as payloads.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\8.png)

<div style="text-align: justify">36. Copy and paste the list and click add.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\9.png)

<div style="text-align: justify">37. Click on Processors.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\10.png)

<div style="text-align: justify">38. Y convertir la lista con los payloads en MD5 Hash.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\11.png)

<div style="text-align: justify">39. Click on Start Fuzzer.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\12.png)

<div style="text-align: justify">40. Sort requests by response size. There is a request with the largest size. Observe the request response and get the flag.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q6\13.png)


## ZAP Scanner

>**Q. un ZAP Scanner on the target above to identify directories and potential vulnerabilities. Once you find the high-level vulnerability, try to use it to read the flag at '/flag.txt'**

<div style="text-align: justify">41. Access the IP in the browser with the ZAP proxy activated in order to capture the request.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q7\1.png)

<div style="text-align: justify">42. In ZAP select the captured request and with the right button click on Attack->Spider.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q7\2.png)

<div style="text-align: justify">43. Two suspicious files are found with the name "ping.php".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q7\3.png)

<div style="text-align: justify">44. The "ping.php" file in the root does not get a response.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q7\4.png)

<div style="text-align: justify">45. The "ping.php" file under the "devtools" directory returns "200 OK".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q7\5.png)

<div style="text-align: justify">46. Select the root directory and with the right button perform an "Active Scan".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q7\6.png)

<div style="text-align: justify">47. ZAP finds a "Remote OS Command Injection" vulnerability in "devtools/ping.php".</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q7\7.png)

<div style="text-align: justify">48. It is verified that the vulnerability exists using the url provided by ZAP.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q7\8.png)

<div style="text-align: justify">49. Changing the URL "etc%2Fpasswd" to "flag.txt", the flag is obtained.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q7\9.png)


## Skills Assessment - Using Web Proxies

>**Q. The /lucky.php page has a button that appears to be disabled. Try to enable the button, and then click it to get the flag.**

<div style="text-align: justify">51. Access the IP of the statement in the web browser with the developer options activated. The code part of the button that is not working is checked.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\1.1.png)

<div style="text-align: justify">52. Remove the code "disabled=""" and click on the button.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\1.2.png)

<div style="text-align: justify">53. The request is captured in BurpSuite and sent to the Repeater.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\1.3.png)

<div style="text-align: justify">54. In the Repeater, send the request several times until you see the flag.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\1.4.png)

>**Q. The /admin.php page uses a cookie that has been encoded multiple times. Try to decode the cookie until you get a value with 31-characters. Submit the value as the answer.**

<div style="text-align: justify">55. Access the administration panel at "/admin.php". Open the developer tools and check that there is a cookie.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\2.png)

<div style="text-align: justify">56. With [CyberChef](https://gchq.github.io/) decode the cookie. Using "From Hex" and "From Base64" as in the image below yields the 31-character hash.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\3.png)

>**Q. Once you decode the cookie, you will notice that it is only 31 characters long, which appears to be an md5 hash missing its last character. So, try to fuzz the last character of the decoded md5 cookie with all alpha-numeric characters, while encoding each request with the encoding methods you identified above. (You may use the "alphanum-case.txt" wordlist from Seclist for the payload)**

<div style="text-align: justify">57. The following script takes a file and adds the previous hash to the beginning of each line.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\4.png)

```bash
#!/bin/bash

echo "file: "
read var1

sed  -i  's|^|hash md5|g' $var1
```

<div style="text-align: justify">58. The following script takes a file and adds the previous hash to the beginning of each line.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\5.png)

<div style="text-align: justify">59. The final payload list after using the script.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\6.png)

```bash
./md5string.sh alphanum-case.txt
```

<div style="text-align: justify">60. Send the request for "/admin.php" to the intruder.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\7.png)

<div style="text-align: justify">62. Select the value of the cookie as payload and "Sniper" as the attack type.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\8.png)

<div style="text-align: justify">63. Load the list of payloads generated with the script "alphanum-case.txt" (modified).</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\9.png)

<div style="text-align: justify">64. In payload processing add the encoding process that has been followed before the decoding process with CyberChef. Start the attack.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\10.png)

<div style="text-align: justify">66. Find the request that changes size and check the response to find the flag.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\11.png)

>**Q. You are using the 'auxiliary/scanner/http/coldfusion_locale_traversal' tool within Metasploit, but it is not working properly for you. You decide to capture the request sent by Metasploit so you can manually verify it and repeat it. Once you capture the request, what is the 'XXXXX' directory being called in '/XXXXX/administrator/..'?**

<div style="text-align: justify">67. In Metasploit look for the statement tool. Put the variable values as in the following image.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\12.png)

<div style="text-align: justify">68. The request is automatically captured in BurpSuite, obtaining the answer to the question.</div><br>
![image-center](\assets\images\HTB_using_web_proxies\Q8\13.png)


