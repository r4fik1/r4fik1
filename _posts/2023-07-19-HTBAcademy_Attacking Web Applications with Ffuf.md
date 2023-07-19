---
title: "[HTB_Academy] Attacking Web Applications with Ffuf"
excerpt: "**Attacking Web Applications with Ffuf** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_attacking_web_applications_with_ffuf/banner.png
  teaser: /assets/images/HTB_attacking_web_applications_with_ffuf/upper.png
  og_image: /assets/images/HTB_attacking_web_applications_with_ffuf/upper.png
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
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\upper.png)

## Disclaimer
<img style="float: left; padding-right:10px" src="\assets\images\disclaimer.png" width="110" height="110">

<div style="text-align: justify">The following post may contain spoilers. Use it as a guide or support. It is always better to try it by yourself!</div>
<div style="text-align: justify">Enjoy :)</div>

## Resources
<img style="float: left; padding-right:10px" src="\assets\images\github.avif" width="110" height="110">
<div style="text-align: justify">All resources can be found in the following GitHub repository:</div>
[R4fik1-HTB_information_gathering_Repository](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_attacking_web_applications_with_ffuf)


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


## Directory Fuzzing

>**Q. In addition to the directory we found above, there is another directory that can be found. What is it?**

<div style="text-align: justify">1. Simply ffuf search for the different directories using the list "directory-list-2.3-small.txt".</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://159.65.81.48:32733/FUZZ
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q1\1.png)

## Page Fuzzing

>**Q. Try to use what you learned in this section to fuzz the '/blog' directory and find all pages. One of them should contain a flag. What is the flag?**

<div style="text-align: justify">2. Use ffuf with the list "web-extensions.txt" pointing to "blog/indexFUZZ" to find the extensions.</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://159.65.81.48:32733/blog/indexFUZZ
```

![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q2\1.png)
<div style="text-align: justify">3. Once the extensions are found, use the list "directory-list-2.3-small.txt" in "blog/FUZZ.php" to find the file with extension ".php".</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://159.65.81.48:32733/blog/FUZZ.php
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q2\2.png)

<div style="text-align: justify">4. Lastly, access the found URL with a web browser or curl to get the flag.</div><br>
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q2\3.png)

## Recursive Fuzzing

>**Q. Try to repeat what you learned so far to find more files/directories. One of them should give you a flag. What is the content of the flag?**

<div style="text-align: justify">5. Using recursion to get directories and extensions</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://159.65.81.48:32733/FUZZ  -recursion -recursion-depth 1 -e .php -v
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q3\1.png)

<div style="text-align: justify">6. In the following image you can see that there is a "flag.php" file.</div><br>
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q3\2.png)

<div style="text-align: justify">7. Accessing from the web browser you get the flag.</div><br>
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q3\3.png)

## Sub-domain Fuzzing

>**Q. HackTheBox has an online Swag Shop. Try running a sub-domain fuzzing test on 'hackthebox.eu' to find it. What is the full domain of it?**

<div style="text-align: justify">8. Using the list "subdomains-top1million-5000.txt" the subdomain is found as in the following image.</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://FUZZ.hackthebox.eu/
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q4\1.png)

## Filtering Results

>**Q. Try running a VHost fuzzing scan on 'academy.htb', and see what other VHosts you get. What other VHosts did you get?**

<div style="text-align: justify">9. Using the list "subdomains-top1million-5000.txt" the subdomain is found as in the following image. To filter use "-fs 986".</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://159.65.81.48:32733/ -H 'Host: FUZZ.academy.htb' -fs 986
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q5\1.png)

## Parameter Fuzzing - GET

>**Q. Using what you learned in this section, run a parameter fuzzing scan on this page. what is the parameter accepted by this webpage?**

<div style="text-align: justify">10. Add "admin.academy.htb" to "/etc/hosts".</div>
```bash
cat /etc/hosts
144.126.206.259 admin.academy.htb
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q6\1.png)

<div style="text-align: justify">11. Using the list "burp-parameter-names.txt" with the filter "-fs 789" on the parameter gets the value of the parameter.</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://admin.academy.htb:32654/admin/admin.php?FUZZ=key -fs 798
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q5\2.png)

## Value Fuzzing

>**Q. Try to create the 'ids.txt' wordlist, identify the accepted value with a fuzzing scan, and then use it in a 'POST' request with 'curl' to collect the flag. What is the content of the flag?**

<div style="text-align: justify">12. Create a list of "ids" from zero to a thousand.</div>
```bash
for i in $(seq 1 1000); do echo $i >> ids.txt; done
ls
cat ids.txt
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q7\1.png)

<div style="text-align: justify">13. Using the above list run ffuf on a post request on the "id" parameter. Filtering with "-fs 768" returns the id value.</div>
```bash
sudo ffuf -w ids.txt:FUZZ -u http://admin.academy.htb:32654/admin/admin.php -X POST -d 'id=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs 768
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q7\2.png)

<div style="text-align: justify">14. Execute the POST request via cur with the above id to get the flag.</div>
```bash
curl -d "id=**" -H 'Content-Type: application/x-www-form-urlencoded' -X POST http://admin.academy.htb:32654/admin/admin.php
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q7\3.png)

## Skills Assessment - Web

>**Q. Run a sub-domain/vhost fuzzing scan on '*.academy.htb' for the IP shown above. What are all the sub-domains you can identify? (Only write the sub-domain name)**

<div style="text-align: justify">15. With the list "subdomains-top1million-5000.txt" and the filter "-fs 985" the subdomains are obtained.</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-5000.txt:FUZZ -u http://178.62.23.66:31001/ -H 'Host: FUZZ.academy.htb' -fs 985
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q8\1.png)

>**Q. Before you run your page fuzzing scan, you should first run an extension fuzzing scan. What are the different extensions accepted by the domains?**

<div style="text-align: justify">16. Add the subdomains to "/etc/hosts".</div><br>
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q8\2.png)

<div style="text-align: justify">17. Run ffuf to find the extensions with the list "web-extensions.txt".</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/web-extensions.txt:FUZZ -u http://faculty.academy.htb:31001/indexFUZZ
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q8\3.png)

>**Q. One of the pages you will identify should say 'You don't have access!'. What is the full page URL?**

<div style="text-align: justify">18. Using the recursion with one of the above extensions returns the file.</div>
```bash
ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/directory-list-2.3-small.txt:FUZZ -u http://faculty.academy.htb:31001/FUZZ  -recursion -recursion-depth 1 -e .php7 -v -fs 0
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q8\4.png)

<div style="text-align: justify">19. Access the link using a web browser to check the message "You don't have access!".</div><br>
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q8\5.png)

>**Q. In the page from the previous question, you should be able to find multiple parameters that are accepted by the page. What are they?**

<div style="text-align: justify">20. Find the name of the parameter with the list "burp-parameter-names.txt".</div>
```bash
sudo ffuf -w /usr/share/wordlists/SecLists/Discovery/Web-Content/burp-parameter-names.txt:FUZZ -u http://faculty.academy.htb:31001/courses/***.php7?FUZZ=key -fs 774
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q8\6.png)


>**Q. Try fuzzing the parameters you identified for working values. One of them should return a flag. What is the content of the flag?**

<div style="text-align: justify">21. With the above information use the list "names.txt" to find the username. Tip: use variations of the one found above as a parameter (such as "username").</div>
```bash
sudo ffuf -w /usr/share/wordlists/dirb/others/names.txt:FUZZ -u http://faculty.academy.htb:31001/courses/***.php7 -X POST -d 'username=FUZZ' -H 'Content-Type: application/x-www-form-urlencoded' -fs 781
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q8\7.png)


<div style="text-align: justify">22. Send a POST request via curl with the above data to get the flag.</div>
```bash
curl -d "username=***" -H 'Content-Type: application/x-www-form-urlencoded' -X POST http://faculty.academy.htb:31001/courses/***.php7
```
![image-center](\assets\images\HTB_attacking_web_applications_with_ffuf\Q8\8.png)