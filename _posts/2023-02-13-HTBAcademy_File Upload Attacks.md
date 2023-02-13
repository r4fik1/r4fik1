---
title: "[HTB_Academy] File Upload Attacks"
excerpt: "**File Upload Attacks** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_File_Upload_Attacks/banner.png
  teaser: /assets/images/HTB_File_Upload_Attacks/upper.png
  og_image: /assets/images/HTB_File_Upload_Attacks/upper.png
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
  - File Upload Attacks
  - PHP
  - Python
  - Bash
  - Shell
layout: single
toc: true
---
![image-center](\assets\images\HTB_File_Upload_Attacks\upper.png)


## Disclaimer
<img style="float: left; padding-right:10px" src="\assets\images\disclaimer.png" width="110" height="110">

<div style="text-align: justify">The following post may contain spoilers. Use it as a guide or support. It is always better to try it by yourself!</div>
<div style="text-align: justify">Enjoy :)</div>

## Resources
<img style="float: left; padding-right:10px" src="\assets\images\github.avif" width="110" height="110">
<div style="text-align: justify">All resources can be found in the following GitHub repository:</div>
[R4fik1-HTB_File_Upload_Attacks_Repository](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)

## Module Summary

<div style="text-align: justify">Many modern web applications have file upload capabilities, which are usually necessary for the web application's functionality to enable features like attaching files or changing a user's profile image. If the file upload functionality is not securely coded, it may be abused to upload arbitrary files to the back-end server, eventually leading to compromise of the back-end server.</div>

<div style="text-align: justify">When an attacker can upload arbitrary files to the back-end server, they can upload malicious files, like web shells, which would enable them to execute arbitrary commands on the back-end server. This eventually allows attackers to take control over the entire server and all web applications hosted on it, which makes File Upload Attacks among the most critical web vulnerabilities.</div>

<div style="text-align: justify">This module will discuss the basics of identifying and exploiting file upload vulnerabilities and identifying and mitigating basic security restrictions in place to reach arbitrary file uploads.</div>

<div style="text-align: justify">In addition to the above, the File Upload Attacks module will teach you the following:</div><br>

  - What are file upload vulnerabilities?
  - Examples of code vulnerable to file upload vulnerabilities
  - Different types of file upload validations
  - Detecting and exploiting basic file upload vulnerabilities
  - Bypassing client-side file upload validation
  - Bypassing blacklisted and whitelisted extension validation
  - Bypassing type and content validation
  - Bypassing other basic security restrictions
  - Attacking upload forms with limited allowed file types
  - Preventing file upload vulnerabilities through secure validation techniques
  
## Absent Validation

>**Q. Try to upload a PHP script that executes the (hostname) command on the back-end server, and submit the first word of it as the answer.**
<div style="text-align: justify">1. Access the target. It is a website that requests an image "Upload to your employee archive".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q1\1.png)

<div style="text-align: justify">2. Create a shell with a ".php" extension to upload instead of an image.</div>
>>You can download the shell from the following link: [shell.php](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q1\2.png)

<div style="text-align: justify">3. Click on "Drag yout file here or click in this area" and upload the shell created in the previous step.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q1\3.png)

<div style="text-align: justify">4. Click on "Upload" and see that the file has been uploaded correctly.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q1\4.png)

<div style="text-align: justify">5. Check the hostname by accessing:</div>
```
http://IP:PORT/uploads/shell.php
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q1\5.png)

## Upload Exploitation

>**Q. Try to exploit the upload feature to upload a web shell and get the content of /flag.txt**

<div style="text-align: justify">1. Access the target. An employee file is requested.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q2\1.png)

<div style="text-align: justify">2. Create a shell with the ".php" extension that allows you to execute commands.</div>
>>You can download the shell from the following link: [shell.php](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q2\2.png)

<div style="text-align: justify">3. Upload the sell created in the previous step by clicking on "Drag you out file here or click in this area", selecting the "shell.php" and clicking on the "Upload" button. The message "File successfully uploaded" is displayed.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q2\3.png)

<div style="text-align: justify">4. Execute the "id" command as a URL parameter by accessing:</div>
```
http://IP:PORT/uploads/shell.php?cmd=id
```

<div style="text-align: justify">5. The UID and GID of the server are displayed, so the command execution works correctly.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q2\4.png)

<div style="text-align: justify">6. Look for a file that can contain the flag with the "ls" command as a URL parameter:</div>
```
http://IP:PORT/uploads/shell.php?cmd=ls ../../../../
```

<div style="text-align: justify">7. The file "flag.txt" is discovered.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q2\5.png)

<div style="text-align: justify">8. Read the content of "flag.txt" with the "cat" command as the URL parameter.</div>
```
http://IP:PORT/uploads/shell.php?cmd=cat ../../../../flag.txt
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q2\6.png)

>>You can download the shell from the following link: [shell.php](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

## Client-Side Validation

>**Q. Try to bypass the client-side file type validations in the above exercise, then upload a web shell to read /flag.txt (try both bypass methods for better practice)**

<div style="text-align: justify">1. Access the target. As in the previous questions, the target asks us to upload a profile image. Open the developer tools and in the "Inspector" tab expand all to see the source code. There are several "Client-Side Validation" that were bypassed in step three.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q3\1.png)

<div style="text-align: justify">2. Create a shell with the ".php" extension that allows you to execute commands.</div>
>>You can download the shell from the following link: [shell.php](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q3\2.png)

<div style="text-align: justify">3. Delete the content of the "accept" parameter. Remove "if(validate())" from the "onsubmit" parameter as seen in the following image. And upload the shell created in the previous step once the client-side validations have been deleted.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q3\3.png)

<div style="text-align: justify">4.  Execute the "ls" command as a URL parameter. The file "flag.txt" is discovered.</div>
```
http://IP:PORT/profile_images/shell.php?cmd=ls ../../../../
```

![image-center](\assets\images\HTB_File_Upload_Attacks\Q3\4.png)
<div style="text-align: justify">5. Read the content of "flag.txt" with the "cat" command as the URL parameter.</div>
```
http://IP:PORT/profile_images/shell.php?cmd=cat ../../../../flag.txt
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q3\5.png)


## Blacklist Filters

>**Q. Try to find an extension that is not blacklisted and can execute PHP code on the web server, and use it to read "/flag.txt"**

<div style="text-align: justify">1. First of all remove "Client-Side Validation" as in the previous question.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\1.png)

<div style="text-align: justify">2. Create a file test.jpg and upload it to be able to capture the request with Burpsuite and send it to the "Burpsuite Intruder".</div>
```bash
echo "test" > test.jpg
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\2.png)

<div style="text-align: justify">3. The type of attack will be "Sniper", the position of the payload will be the extension of the file uploaded in the previous step of the "filename" parameter.</div>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\3.png)

<div style="text-align: justify">4. In the payload options, uncheck the "URL-encode" option and load the following list (different combinations are also added)</div><br>
>>[PHP extension list](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Upload%20Insecure%20Files/Extension%20PHP/extensions.lst)

![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\4.png)

<div style="text-align: justify">5. Execute the attack. It is appreciated that the responses of the requests have different lengths (193 or 188).</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\5.png)

<div style="text-align: justify">6. The response of the request with length 188 is "Extension not allowed".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\6.png)

<div style="text-align: justify">7. The response of the request with length 193 is "File successfully uploaded". So the extension ".phar" is allowed.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\7.png)

<div style="text-align: justify">8. Create a shell with the ".phar" extension that allows you to execute commands.</div>
>>You can download the shell from the following link: [shell.php](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\8.png)

<div style="text-align: justify">9. Upload the "shell.phar" file created in the previous step. Capture the request with Burpsuite and see that the file has been uploaded correctly.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\9.png)

<div style="text-align: justify">10. Execute the "ls" command as a URL parameter. The file "flag.txt" is discovered.</div>
```
http://IP:PORT/profile_images/shell.phar?cmd=ls ../../../../
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\10.png)

<div style="text-align: justify">11. Read the content of "flag.txt" with the "cat" command as the URL parameter.</div>
```
http://IP:PORT/profile_images/shell.phar?cmd=cat ../../../../flag.txt
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q4\11.png)



## Whitelist Filters

>**Q. The above exercise employs a blacklist and a whitelist test to block unwanted extensions and only allow image extensions. Try to bypass both to upload a PHP script and execute code to read "/flag.txt"**

<div style="text-align: justify">1. Access the target. As in the previous questions, the target asks us to upload a profile image. Open the developer tools and in the "Inspector" tab expand all to see the source code. There are several "Client-Side Validation" that were bypassed in next step.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\1.png)

<div style="text-align: justify">2. Delete the content of the "onchange" and "accept" parameters, with this the function that checks the uploaded file is deleted as well as the extensions accepted on the client side.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\2.png)

<div style="text-align: justify">3. Create a file test.jpg and upload it to be able to capture the request with Burpsuite and send it to the "Burpsuite Intruder".</div>
```bash
echo "test" > test.jpg
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\3.png)

<div style="text-align: justify">4. The type of attack will be "Sniper", the position of the payload will be the extension of the file uploaded in the previous step of the "filename" parameter.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\4.png)

<div style="text-align: justify">5. In the payload options, uncheck the "URL-encode" option and load the following list (different combinations are also added)</div>
>>[PHP extension list](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Upload%20Insecure%20Files/Extension%20PHP/extensions.lst)

![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\5.png)

<div style="text-align: justify">6. Execute the attack. It is appreciated that the responses of the requests have different lengths (193, 190 or 188).The response of the request with length 188 is "Extension not allowed".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\6.png)

<div style="text-align: justify">7. The response of the request with length 190 is "Only images are allowed".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\7.png)

<div style="text-align: justify">8. The response of the request with length 193 is "File successfully uploaded". So it checks that files with extensions ending in "\x00.gif", "\x00.png" and "\x00.jpg" are allowed.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\8.png)

<div style="text-align: justify">9. Since we know that the file has to end in an extension like ".jpg" and that the extension ".phar" returns a different error, we create a script with the extension ".phar.jpg".</div>
>>You can download the shell from the following link: [shell.phar.jpg](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\9.png)

<div style="text-align: justify">10. Go back to the target and upload the shell created in the previous step with the extension ".phar.jpg".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\10.png)

<div style="text-align: justify">11. The shell is successfully uploaded.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\11.png)

<div style="text-align: justify">12. Execute the "ls" command as a URL parameter. The file "flag.txt" is discovered.</div>
```
http://IP:PORT/profile_images/shell.phar?cmd=ls ../../../../
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\12.png)

<div style="text-align: justify">13. Read the content of "flag.txt" with the "cat" command as the URL parameter.</div>
```
http://IP:PORT/profile_images/shell.phar?cmd=cat ../../../../flag.txt
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q5\13.png)

## Type Filters

>**Q. The above server employs Client-Side, Blacklist, Whitelist, Content-Type, and MIME-Type filters to ensure the uploaded file is an image. Try to combine all of the attacks you learned so far to bypass these filters and upload a PHP file and read the flag at "/flag.txt"**

<div style="text-align: justify">1. Access the target. As in the previous questions, the target asks us to upload a profile image. Open the developer tools and in the "Inspector" tab expand all to see the source code. There are several "Client-Side Validation" that were bypassed in step three.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\1.png)

<div style="text-align: justify">2. Download a test image with a ".jpg" extension to upload it and later capture the request with Burpsuite.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\2.png)

<div style="text-align: justify">3. Delete the content of the "onchange" and "accept" parameters, with this the function that checks the uploaded file is deleted as well as the extensions accepted on the client side.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\3.png)

<div style="text-align: justify">4. Upload the test image to capture the request in Burpsuite.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\4.png)

<div style="text-align: justify">5. In the screenshot you can see the "filename" parameter with the name of the image and its extension. You also see the "Content-Type" parameter with the value "image/jpeg", as well as the "MIME-Type" in the first bytes of the file content. We send the request to the "Burpsuite Intruder".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\5.png)

<div style="text-align: justify">6. The type of attack will be "Sniper", the position of the payload will be the extension of the file uploaded in the previous step of the "filename" parameter.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\6.png)

<div style="text-align: justify">7. In the payload options, uncheck the "URL-encode" option and load the following list (different combinations are also added)</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\7.png)

<div style="text-align: justify">8. Execute the attack. It is appreciated that the responses of the requests have different lengths (193, 190 or 188).The response of the request with length 188 is "Extension not allowed".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\8.png)

<div style="text-align: justify">9. The response of the request with length 190 is "Only images are allowed".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\9.png)

<div style="text-align: justify">10. The response of the request with length 193 is "File successfully uploaded". So it checks that files with extensions ending in "\x00.gif", "\x00.png" and "\x00.jpg" are allowed.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\10.png)

<div style="text-align: justify">11. Since we know that the file has to end in an extension like ".gif" and that the extension ".phar" returns a different error, we create a script with the extension ".phar.gif". We also add "GIF8" as the first few bits in the shell.</div>
>>You can download the shell from the following link: [shell.gif.phar](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\11.png)

<div style="text-align: justify">12. Go back to the target and upload the shell created in the previous step with the extension ".phar.jpg". We see in Burpsuite how the shell has been uploaded correctly (file extension, MIME-Type and Content-Type) but it cannot be executed.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\12.png)

<div style="text-align: justify">13. Several intermediate steps need to be performed before executing the shell. We send the previous request to the "Burpsuite Repeater".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\13.png)

<div style="text-align: justify">14 We copy the content of the created shell to a new shell with the extensions swapped (from "shell.phar.gif" to "shell.gif.phar").</div>
>>You can download the shell from the following link: [shell.phar.gif](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

```bash
cp shell.phar.gif shell.gif.phar
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\14.png)

<div style="text-align: justify">15. In the request sent in step 13 to the "Burpsuite Repeater" change the extension of the value of the "filename" parameter: from "shell.phar.gif" to "shell.gif.phar". And send the request.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\15.png)

<div style="text-align: justify">16. Execute the "ls" command as a URL parameter. The file "flag.txt" is discovered.</div>
```
http://IP:PORT/profile_images/shell.phar?cmd=ls ../../../../
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\16.png)

<div style="text-align: justify">17. Read the content of "flag.txt" with the "cat" command as the URL parameter.</div>
```
http://IP:PORT/profile_images/shell.phar?cmd=cat ../../../../flag.txt
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q6\17.png)




## Limited File Uploads

>**Q. The above exercise contains an upload functionality that should be secure against arbitrary file uploads. Try to exploit it using one of the attacks shown in this section to read "/flag.txt"**

<div style="text-align: justify">1. When accessing the target, the source code shows that it only accepts files with the ".svg" extension.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\1.png)

<div style="text-align: justify">2. Create a shell with the extension ".svg" with an "xml" payload that allows reading files on the server.</div>
>>You can download the shell from the following link: [shell.svg](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\2.png)

<div style="text-align: justify">3. Upload the created shell to the target.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\3.png)

<div style="text-align: justify">4. Click on upload and in the "Inspector" of the developer tools the request with the shell has returned the content of the file requested in the shell "/etc/passwd".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\4.png)

<div style="text-align: justify">5. Modify the shell created in step 2 to read the content of "flag.txt".</div>
>>You can download the shell from the following link: [shell2.svg](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br> 

![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\5.png)

<div style="text-align: justify">6. In the same way as in step 4 we see the content of "flag.txt".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\6.png)




>**Q. Try to read the source code of 'upload.php' to identify the uploads directory, and use its name as the answer. (write it exactly as found in the source, without quotes)

<div style="text-align: justify">1. To use XXE to read source code in PHP web applications, we can use the following payload in our SVG image:</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\7.png)

<div style="text-align: justify">Once the SVG image is displayed, we should get the base64 encoded content of upload.php, which we can decode to read the source code.</div>
>>You can download the shell from the following link: [shell3.svg](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

<div style="text-align: justify">2. We upload the shell created in the previous step.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\8.png)

<div style="text-align: justify">3. Get the source code of "upload.php" encoded in Base64.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\9.png)

<div style="text-align: justify">4. Decode with the Burpsuite Decoder and we get the answer.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q7\10.png)





## Skills Assessment - File Upload Attacks

>**Q. Try to exploit the upload form to read the flag found at the root directory "/".**

<div style="text-align: justify">1. Access the target, explore the application and click on "Contact Us".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\1.png)

<div style="text-align: justify">2. There is a form with different fields but the interesting field is the one that allows you to upload files. Open the developer tools. There is a validation on the client side that will be removed later. There are also two buttons to upload the image, exploring the source code we see that the correct one is the green button.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\2.png)

<div style="text-align: justify">3. We remove the validation on the client side by removing the content of the "onchange" and "accept" parameters.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\3.png)

<div style="text-align: justify">4. Upload a test image with a ".jpg" extension.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\4.png)

<div style="text-align: justify">5. The image is uploaded successfully.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\5.png)

<div style="text-align: justify">6. Capture the request to upload the image with Burpsuite and send it to "Burpsuite Intruder".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\6.png)

<div style="text-align: justify">7. The position of the payload will be the extension of the image (parameter "filename") and the type of attack "Sniper".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\7.png)

<div style="text-align: justify">8. In the payload options, uncheck the "URL-encode" option and load the following list (different combinations are also added)</div>
>>[PHP extension list](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Upload%20Insecure%20Files/Extension%20PHP/extensions.lst)

![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\8.png)

<div style="text-align: justify">9. Execute the attack. We can see that the responses of the requests have different lengths (23216, 190 or 188). The response with length 23216 is the uploaded image.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\9.png)

<div style="text-align: justify">10. The response of the request with length 190 is "Only images are allowed".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\10.png)

<div style="text-align: justify">11. The response of the request with length 188 is "Extension not allowed".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\11.png)

<div style="text-align: justify">12. Create a shell with the allowed extension ".svg" with an xml payload that returns the source code of "upload.php" in Base64.</div>
>>You can download the shell from the following link: [shell.svg](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\12.png)

<div style="text-align: justify">13. Upload the shell.svg created in the previous step.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\13.png)

<div style="text-align: justify">14. In the captured request we see that the response is a Base64 string.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\14.png)

<div style="text-align: justify">15. Paste the Base64 string into the "Burpsuite Decoder" and decode as Base64. We get the source code of upload.php.</div>
>>You can download the "upload.php" file from the following link: [upload.php](https://github.com/r4fik1/HTB_Academy/blob/main/HTB_File_Upload_Attacks/Skill%20Assessment%20-%20File%20Upload%20Attacks/upload.php)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\15.png)

<div style="text-align: justify">16. Analyze the source code of "upload.php".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\16.png)

- (1) Blacklist Filter -> filter not allowing php, phps or phtml extensions.
- (2) Whitelist Filter -> filter that only allows extensions ending in "g".
- (3) Type Filter -> filter that allows images in the Content-Type. The MIME-Type is not yet known as it is filtered.
- (4) common-functions.php -> There is another interesting file.
- (5) Image upload directory.
- (6) Name format of uploaded images.

<div style="text-align: justify">17. Create a shell with the allowed extension ".svg" with an xml payload that returns the source code of "common-functions.php" in Base64.</div>
>>You can download the shell from the following link: [shell2.svg](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\17.png)

<div style="text-align: justify">18. Upload the shell.svg created in the previous step.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\18.png)

<div style="text-align: justify">19. In the captured request we see that the response is a Base64 string.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\19.png)

<div style="text-align: justify">20. Paste the Base64 string into the "Burpsuite Decoder" and decode as Base64. We get the source code of common-functions.php.php.</div>
>>You can download the "common-functions.php" file from the following link: [common-functions.php](https://github.com/r4fik1/HTB_Academy/blob/main/HTB_File_Upload_Attacks/Skill%20Assessment%20-%20File%20Upload%20Attacks/common-functions.php)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\20.png)

<div style="text-align: justify">21. Analyze the source code of "common-functions.php". This file is the MIME-Type filter.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\21.png)

<div style="text-align: justify">22. With all the information collected we create a shell that can bypass all the filters.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\22.png)

- In step 9 we see that the extension ".phar.jpeg" is allowed since the response shows the image sent.
- To bypass the MIME-Type and Content-Type filters, copy the content of "image.jpg" to the shell with the extension ".phar.jpeg". Delete all but the first few bytes.
- Introduce a payload in PHP that allows reading files on the server.

```bash
cp image.jpg shell.phar.jpeg
```

<div style="text-align: justify">23. Shell content.</div>
>>You can download the shell from the following link: [shell.phar.jpeg](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_File_Upload_Attacks)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\23.png)

<div style="text-align: justify">24. Upload the shell "shell.phar.jpeg".</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\24.png)
<br>

![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\25.png)

<div style="text-align: justify">25. We see on the frontend that the shell has been successfully uploaded.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\26.png)

<div style="text-align: justify">26. We also see the request in the Burpsuite and how it has been successfully uploaded.</div><br>
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\27.png)

<div style="text-align: justify">27. With the information of the path where the images are located and the name format they have, execute the url with the "cmd" parameter so that it executes an "ls" command in the root. We see a text file with the name of "flag_xxxx.txt".</div>

```
http://IP:PORT/contact/user_feedback_submissions/YYMMDD_shell.phar.jpeg?cmd=ls ../../../../../
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\28.png)

<div style="text-align: justify">28. Execute the url with the "cmd" parameter so that it executes an "cat" command to the file "flag_xxxx.txt" and we get de flag.</div>

```
http://IP:PORT/contact/user_feedback_submissions/YYMMDD_shell.phar.jpeg?cmd=cat ../../../../../flag_xxxx.txt
```
![image-center](\assets\images\HTB_File_Upload_Attacks\Q8\29.png)







