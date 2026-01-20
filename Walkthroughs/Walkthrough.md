# <div align="center">OWASP Top 10 2025 All Rooms — TryHackMe Walkthrough</div>

# Introduction

The **OWASP Top 10 2025** rooms are designed to teach you about the Top10 vulnerabilities that have affected companies in 2025. What they are, how they can be exploited, and how to fix them.

* **Room link**: [https://tryhackme.com/module/owasp-top-10-2025](https://tryhackme.com/module/owasp-top-10-2025)

## OWASP Top 10 2025: IAAA Failures

Here we focus on 3 vulnerabilities: A01, A07, A09

### Task 1: Introduction

	No Answer Needed

### Task 2: What is IAAA

    Identity, Authentication, Authorization, Accountability

### Task 3: A01 Broken Access Control

It is a simple directory traversal, where you are able to change the id value to access different accounts without proper authorization

<div align="center">
  <img width="702" height="590" alt="image" src="https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20IAAA%20Failures/A01/A01.jpg" />
</div>

### Task 4: A07: Authentication Failures

Create a new account that looks similar to the “admin” username. The problem here is that it doesn’t verify capitalizations, so if you capitalize random letters of the username, the site will still redirect you to the admin account which has the flag

<div align="center">
  <img width="702" height="590" alt="image" src="https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20IAAA%20Failures/A07/web1.jpg" />
</div>

<div align="center">
  <img width="702" height="590" alt="image" src="https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20IAAA%20Failures/A07/flag.jpg" />
</div>

### Task 5: A09: Logging & Alerting Failures

This is a simple event log to look through. Note the timeline descends for recent activities, I thought it was the other way around for a second. But looking through the logs gives you the answers easily.

<div align="center">
  <img width="702" height="590" alt="image" src="https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20IAAA%20Failures/A09/flag.jpg" />
</div>


### Task 6: Conclusion
    No Answer Needed


##  OWASP Top 10 2025: Application Design Flaws

### Task 1: Introduction
    No Answer Needed

### Task 2: AS02: Security Misconfigurations

    http://MachineIP:5002

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS02/web1.jpg />
</div>

Here you just need to mess around with the user ID, it only validates and checks for numerical ids, so if you add alphanumeric characters, the webpage breaks, giving you the flag.

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS02/web2.jpg />
</div>

### Task 3: AS03: Software Supply Chain Failures

    http://MachineIP:5003

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS03/web1.jpg />
</div>

Webpages, by default use GET to receive information, but for this flag, we need to access the process, which is only available in POST. So, open **BurpSuite** and enable **FoxyProxy** to capture the */api/process* information.

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS03/web2.jpg />
</div>

Find the request for the */api/process* on **BurpSuite** and send it to the **Repeater**

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS03/Supplychain%201.jpg />
</div>

Now we look at the python code, that is included, the important section is highlighted in red, under the process class. This tells us that if we send a JSON content where *“data” = “debug”*, it will reveal information about the API

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS03/Coe.png />
</div>

Modify the request to **POST**, add in *Content-Type* Information (The information is in json format). At the very bottom, add the actual content/payload. For this task it will be {“data”:”debug”}. This will reveal the flag:

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS03/Supplychain%203.jpg />
</div>

### Task 4: AS04: Cryptographic Failures

    http://MachineIP:5004
Inspect the element of the page and you will notice, there is a *decrypt.js* file that looks promising.

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS04/web1.jpg />
</div>

Then on the page click on inspect page source. At the very bottom of the page, you will see a hyperlink to the *decrypt.js* code. Click on it and look through the file's code.

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS04/web3.jpg />
</div>

On the codes page, look through the *Configuration section*. There are 2 key pieces of information, the **Secret_Key** and the **ENCRYPTION_MODE**

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS04/web4.jpg />
</div>

Now we go to **CyberChef** with this information. Put a *From Base64* block then a *AES Decrypt* block configured with the Secret_key and ECB Mode. Then Copy and Paste the Encrypted Document in the Input and obtain the **flag** from the output.

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS04/Cyberchef.jpg />
</div>

### Task 5: AS06: Insecure Design

    http://MachineIP:5005

Look through the webpage, inspect its network requests, source code, all of it will reveal that the download button is a dead button, and there are no other links that are explicitly revealed/available.

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS06/we1.jpg />
</div>

Now open your **shell** and open **gobuster** with the following command:

    gobuster dir -u http://10.49.160.9:5005/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt

Unfortunately, My attackbox didnt have enough time to fully show the results, but you should see 2 results. One of them should be *users* or *messages*

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS06/GoBuster.jpg />
</div>

Go to the */api/users* to see all the users that are using the app.

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS06/web2.jpg />
</div>

Now traverse through */api/messages/**user***, replacing **user** with the different users found under the */api/users*. You will eventually find that */api/messages/admin* will reveal the flag.

<div align="center">
  <img width="702" height="590" alt="image" src=https://github.com/abheekmondal/THM_Walkthroughs/blob/main/Assets/OWASP%20Top%2010%202025%20Application%20Design%20Flaws/AS06/we2Flag.jpg />
</div>

### Task 6: Conclusion
    No Answer Needed

## Conclusion

This was a straightforward reversing challenge with a small twist at the start. Fixing the binary header and analyzing the password check was enough to reach the flag without overcomplicating things.

**Thank you for reading.**


```
hexedit 0x41haz-1640335532346.0x41haz
```
<div align="center">
  <img width="702" height="590" alt="image" src="https://github.com/user-attachments/assets/ed6d0581-db72-4e4d-bd0e-404010467680" />
</div>
