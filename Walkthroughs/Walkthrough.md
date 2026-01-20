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


##  OWASP Top 10 2025: IAAA Failures

### Task 1: Introduction
    No Answer Needed

### Task 2: AS02: Security Misconfigurations
### Task 3: AS03: Software Supply Chain Failures
### Task 4: AS04: Cryptographic Failures
### Task 5: AS06: Insecure Design
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
