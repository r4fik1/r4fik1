---
title: "Hacking WordPress"
excerpt: "**Hacking WordPress** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_Hacking_WordPress/banner.png
  teaser: /assets/images/HTB_Hacking_WordPress/upper.jpg
  og_image: /assets/images/HTB_Hacking_WordPress/upper.jpg
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
---
![image-center](\assets\images\HTB_Hacking_WordPress\upper.jpg)
## Module Summary

As an information security professional, it is important to understand networking, operating systems, databases, web applications, scripting and programming languages, and more. During the course of your career, you will most likely come in contact with a variety of different types of web applications. As you become more experienced, you will start to see some of the web applications repeatedly, whether from the standpoint of an attacker or a defender. One of the most common web applications used by all sizes and types of organizations is WordPress. This module's goal is to impart a deep understanding of how WordPress websites function to better position them to attack and defend them. In this module, we will cover:

  - An overview of WordPress and the structure of a WordPress website
  - Manual and automated enumeration techniques
  - Attacks against WordPress users
  - Manual and automated attacks against a WordPress installation and the underlying webserver
  - Security hardening best practices to defend against the techniques covered in this module

## Directory Indexing

>*Q. Keep in mind the key WordPress directories discussed in the WordPress Structure section. Manually enumerate the target for any directories whose contents can be listed. Browse these directories and locate a flag with the file name flag.txt and submit its contents as the answer.

## Login

>*Q. Search for "WordPress xmlrpc attacks" and find out how to use it to execute all method calls. Enter the number of possible method calls of your target as the answer.

## WPScan Overview

>*Q. 

## WPScan Enumeration

>*Q. Enumerate the provided WordPress instance for all installed plugins. Perform a scan with WPScan against the target and submit the version of the vulnerable plugin named “photo-gallery”.

## Exploiting a Vulnerable Plugin

>*Q. Use the same LFI vulnerability against your target and read the contents of the "/etc/passwd" file. Locate the only non-root user on the system with a login shell.

## Attacking WordPress Users

>*Q. Perform a bruteforce attack against the user "roger" on your target with the wordlist "rockyou.txt". Submit the user's password as the answer.

## RCE via the Theme Editor

>*Q. Use the credentials for the admin user [admin:sunshine1] and upload a webshell to your target. Once you have access to the target, obtain the contents of the "flag.txt" file in the home directory for the "wp-user" directory.

## Skills Assessment - WordPress

>*Q. Identify the WordPress version number.

>*Q. Identify the WordPress theme in use.

>*Q. Submit the contents of the flag file in the directory with directory listing enabled.

>*Q. Identify the only non-admin WordPress user. (Format: <first-name> <last-name>)

>*Q. Use a vulnerable plugin to download a file containing a flag value via an unauthenticated file download.

>*Q. What is the version number of the plugin vulnerable to an LFI?

>*Q. Use the LFI to identify a system user whose name starts with the letter "f".

>*Q. Obtain a shell on the system and submit the contents of the flag in the /home/erika directory.
