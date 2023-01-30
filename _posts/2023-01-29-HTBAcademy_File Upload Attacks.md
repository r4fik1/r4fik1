---
title: "File Upload Attacks"
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
---
![image-center](\assets\images\HTB_File_Upload_Attacks\upper.png)
## Module Summary

Many modern web applications have file upload capabilities, which are usually necessary for the web application's functionality to enable features like attaching files or changing a user's profile image. If the file upload functionality is not securely coded, it may be abused to upload arbitrary files to the back-end server, eventually leading to compromise of the back-end server.

When an attacker can upload arbitrary files to the back-end server, they can upload malicious files, like web shells, which would enable them to execute arbitrary commands on the back-end server. This eventually allows attackers to take control over the entire server and all web applications hosted on it, which makes File Upload Attacks among the most critical web vulnerabilities.

This module will discuss the basics of identifying and exploiting file upload vulnerabilities and identifying and mitigating basic security restrictions in place to reach arbitrary file uploads.

In addition to the above, the File Upload Attacks module will teach you the following:

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

>*Q. Try to upload a PHP script that executes the (hostname) command on the back-end server, and submit the first word of it as the answer.

## Upload Exploitation

>*Q. Try to exploit the upload feature to upload a web shell and get the content of /flag.txt

## Client-Side Validation

>*Q. Try to bypass the client-side file type validations in the above exercise, then upload a web shell to read /flag.txt (try both bypass methods for better practice)

## Blacklist Filters

>*Q. Try to find an extension that is not blacklisted and can execute PHP code on the web server, and use it to read "/flag.txt"

## Whitelist Filters

>*Q. The above exercise employs a blacklist and a whitelist test to block unwanted extensions and only allow image extensions. Try to bypass both to upload a PHP script and execute code to read "/flag.txt"

## Type Filters

>*Q. The above server employs Client-Side, Blacklist, Whitelist, Content-Type, and MIME-Type filters to ensure the uploaded file is an image. Try to combine all of the attacks you learned so far to bypass these filters and upload a PHP file and read the flag at "/flag.txt"

## Limited File Uploads

>*Q. The above exercise contains an upload functionality that should be secure against arbitrary file uploads. Try to exploit it using one of the attacks shown in this section to read "/flag.txt"
>*Q. Try to read the source code of 'upload.php' to identify the uploads directory, and use its name as the answer. (write it exactly as found in the source, without quotes)

## Skills Assessment - File Upload Attacks

>*Q. Try to exploit the upload form to read the flag found at the root directory "/".