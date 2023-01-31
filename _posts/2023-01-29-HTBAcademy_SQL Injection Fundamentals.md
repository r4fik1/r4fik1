---
title: "SQL Injection Fundamentals"
excerpt: "**SQL Injection Fundamentals** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_SQL_Injection_Fundamentals/banner.png
  teaser: /assets/images/HTB_SQL_Injection_Fundamentals/upper.jpg
  og_image: /assets/images/HTB_SQL_Injection_Fundamentals/upper.jpg
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - OWASP TOP 10
layout: single
toc: true
---
![image-center](\assets\images\HTB_SQL_Injection_Fundamentals\upper.jpg)
## Module Summary


Database Management systems offer faster storage and retrieval of data in comparison to traditional file storage. This makes them the medium of choice for storing data such as credentials, posts, and comments used by web applications. However, improperly implemented SQL logic can be dangerous and can lead to authentication bypass, information disclosure, remote code execution, and total server compromise.

Applications implement code to create SQL queries to interact with databases. These queries can incorporate user input, which may not be properly sanitized. This leads to the creation of queries that cause unintended actions other than what the developer expected.

This module aims to develop the skills necessary to identify and exploit SQL injection vulnerabilities, mainly for MySQL databases, and as an intro to all other types of SQL injections.

In this module, we will cover the following topics:

  - Basics of databases and their different types
  - Basics of SQL and MySQL
  - Basic statements and operators in MySQL and how to use them
  - What are SQL injections, and how can we use them
  - Use SQL injections to subvert the web application logic and bypass authentication
  - Use UNION SQL injections to dump data from different tables and databases within the DBMS
  - Use SQL injections to read files of the back-end server
  - Use SQL injections to write a web shell on the back-end server and gain remote control over it
  - How to mitigate such SQL injections and patch your code

## Intro to MySQL

>*Q. Connect to the database using the MySQL client from the command line. Use the 'show databases;' command to list databases in the DBMS. What is the name of the first database?

## SQL Statements

>*Q. What is the department number for the 'Development' department?

## Query Results

>*Q. What is the last name of the employee whose first name starts with "Bar" AND who was hired on 1990-01-01?

## SQL Operators

>*Q. In the 'titles' table, what is the number of records WHERE the employee number is greater than 10000 OR their title does NOT contain 'engineer'?

## Subverting Query Logic

>*Q. Try to log in as the user 'tom'. What is the flag value shown after you successfully log in?

## Using Comments

>*Q. Login as the user with the id 5 to get the flag.

## Union Clause

>*Q. Connect to the above MySQL server with the 'mysql' tool, and find the number of records returned when doing a 'Union' of all records in the 'employees' table and all records in the 'departments' table.

## Union Injection

>*Q. Use a Union injection to get the result of 'user()'

## Database Enumeration

>*Q. What is the password hash for 'newuser' stored in the 'users' table in the 'ilfreight' database?

## Reading Files

>*Q. We see in the above PHP code that '$conn' is not defined, so it must be imported using the PHP include command. Check the imported page to obtain the database password.

## Writing Files

>*Q. Find the flag by using a webshell.

## Skills Assessment - SQL Injection Fundamentals

>*Q. Assess the web application and use a variety of techniques to gain remote code execution and find a flag in the / root directory of the file system. Submit the contents of the flag as your answer.