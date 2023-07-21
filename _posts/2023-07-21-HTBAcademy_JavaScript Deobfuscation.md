---
title: "[HTB_Academy] JavaScript Deobfuscation"
excerpt: "**JavaScript Deobfuscation** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_javascript_deobfuscation/banner.png
  teaser: /assets/images/HTB_javascript_deobfuscation/upper.jpeg
  og_image: /assets/images/HTB_javascript_deobfuscation/upper.jpeg
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
![image-center](\assets\images\HTB_javascript_deobfuscation\upper.jpeg)

## Disclaimer
<img style="float: left; padding-right:10px" src="\assets\images\disclaimer.png" width="110" height="110">

<div style="text-align: justify">The following post may contain spoilers. Use it as a guide or support. It is always better to try it by yourself!</div>
<div style="text-align: justify">Enjoy :)</div>

## Resources
<img style="float: left; padding-right:10px" src="\assets\images\github.avif" width="110" height="110">
<div style="text-align: justify">All resources can be found in the following GitHub repository:</div>
[R4fik1-HTB_broken_authentication_Repository](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_javascript_deobfuscation)

## Module Summary

Many malicious actors tend to obfuscate their code to avoid it being detected by systems or understood by other developers.

The ability to deobfuscate code is a useful technique that can be applied to various real-world scenarios. It is useful on web application assessments to determine if a developer has used "security by obscurity" to hide JavaScript code containing sensitive data. It can also be useful for defenders when, for example, attempting to deobfuscate code that was responsible for the Phishing website used in an attack.

In this module, you will learn the basics of deobfuscating and decoding JavaScript code and will have several exercises to practice what you learned.

You will learn the following topics:

  - Locating JavaScript code
  - Intro to Code Obfuscation
  - How to Deobfuscate JavaScript code
  - How to decode encoded messages
  - Basic Code Analysis
  - Sending basic HTTP requests
  
## Source Code

>**Q. Repeat what you learned in this section, and you should find a secret flag, what is it?**

<div style="text-align: justify">1. Open the target in a web browser, right click and open the source code. The flag is in a code comment.</div><br>
![image-center](\assets\images\HTB_javascript_deobfuscation\Q1\1.png)

## Deobfuscation

>**Q. Using what you learned in this section, try to deobfuscate 'secret.js' in order to get the content of the flag. What is the flag?**

<div style="text-align: justify">2. In the source code there is a direct link to a "js" file. Click on it.</div><br>
![image-center](\assets\images\HTB_javascript_deobfuscation\Q2\1.png)

<div style="text-align: justify">3. This file has an unreadable code.</div><br>
![image-center](\assets\images\HTB_javascript_deobfuscation\Q2\2.png)

<div style="text-align: justify">4. Access "JSNice" and click on "Nicify JavaScript". The flag is found in the ordered code.</div><br>
[jsnice Link](http://www.jsnice.org/)
![image-center](\assets\images\HTB_javascript_deobfuscation\Q2\3.png)

## HTTP Requests

>**Q.  Try applying what you learned in this section by sending a 'POST' request to '/serial.php'. What is the response you get?**

<div style="text-align: justify">5. Perform a POST request using curl to "serial.php".</div>
```bash
curl -s http://83.136.250.34:34154/serial.php -X POST
```
![image-center](\assets\images\HTB_javascript_deobfuscation\Q3\1.png)

## Decoding

>**Q. Using what you learned in this section, determine the type of encoding used in the string you got at previous exercise, and decode it. To get the flag, you can send a 'POST' request to 'serial.php', and set the data as "serial=YOUR_DECODED_OUTPUT".**

<div style="text-align: justify">6. Decode from base64 into previous string. Make a POST request using curl with the value of the decoded serial parameter.</div><br>
![image-center](\assets\images\HTB_javascript_deobfuscation\Q4\1.png)

## Skills Assessment

>**Q. Try to study the HTML code of the webpage, and identify used JavaScript code within it. What is the name of the JavaScript file being used?**

<div style="text-align: justify">7. Access the source code and look for the ".js" file.</div><br>
![image-center](\assets\images\HTB_javascript_deobfuscation\Q5\1.png)

>**Q. Once you find the JavaScript code, try to run it to see if it does any interesting functions. Did you get something in return?**

<div style="text-align: justify">8. Access the previous file and view the source code in the web browser.</div><br>
![image-center](\assets\images\HTB_javascript_deobfuscation\Q5\2.png)

<div style="text-align: justify">9. Using "JSNice" tidies up the code and makes it readable.</div>
[jsnice Link](http://www.jsnice.org/)

![image-center](\assets\images\HTB_javascript_deobfuscation\Q5\3.png)

<div style="text-align: justify">10. Run the code at "PlayCode" and the output will be the flag.</div> 
[PlayCode Link](https://playcode.io/javascript)

![image-center](\assets\images\HTB_javascript_deobfuscation\Q5\4.png)


>**Q. As you may have noticed, the JavaScript code is obfuscated. Try applying the skills you learned in this module to deobfuscate the code, and retrieve the 'flag' variable.**

<div style="text-align: justify">11. The flag is the content of the "flag" variable.</div><br>
![image-center](\assets\images\HTB_javascript_deobfuscation\Q5\4.1.png)

>**Q. Try to Analyze the deobfuscated JavaScript code, and understand its main functionality. Once you do, try to replicate what it's doing to get a secret key. What is the key?**

<div style="text-align: justify">12. In the code you see a file "key.php"</div><br>
![image-center](\assets\images\HTB_javascript_deobfuscation\Q5\5.png)

<div style="text-align: justify">13. Make a POST request using curl pointing to the file "keys.php" as seen in the code and get the key.</div>
```bash
curl -s http://94.237.62.6:35342/keys.php -X POST
```
![image-center](\assets\images\HTB_javascript_deobfuscation\Q5\6.png)

>**Q. Once you have the secret key, try to decide it's encoding method, and decode it. Then send a 'POST' request to the same previous page with the decoded key as "key=DECODED_KEY". What is the flag you got?**

<div style="text-align: justify">14. Decode the above string with "xxd -p -r". Use the decrypted key to make a POST request by passing the value before the "key" parameter.</div>
```bash
echo 4150495f70336e5f37333537316e3 | xxd -p -r

curl http://94.237.62.6:35342/keys.php -X POST -d "key=API_p3n_73571n6_15_fun"
```
![image-center](\assets\images\HTB_javascript_deobfuscation\Q5\7.png)