---
image: /assets/img/brute-it/brute-it.png
title: "[CTF] Brute It - THM "
description: "Learn how to brute, hash cracking and escalate privileges in this box!"
date: 2024-09-09 22:08:00 +0000
categories: [ctf]
tags: [ctf, write-up, tryhackme]
---

# Brute It Write-Up
Hi there! This write-up about [Brute It](https://tryhackme.com/r/room/bruteit)  on [TryHackMe](https://tryhackme.com/). Brute-It is an easy level room, so this is ideal for beginners and newbies.

## Task 1 - Deploy The Machine
Deploy the machine and go.

## Task 2 - Reconnaissance
Use **NMAP** to start a port scan and get their versions.


![nmap-scan](assets/img/brute-it/brute-it-nmap.png)
 We got the answers of the first 4 questions. 

---

Then we should find the hidden directory. You can use the your favorite directory scan tool. I am using **Dirb** because it is very easy to use.
![dirb-scan](assets/img/brute-it/brute-it-dirb.png)

## Task 3 - Getting A Shell
We found a login page on the *hidden* directory.
![nmap-scan](assets/img/brute-it/brute-it-hidden.png)

I have seen a comment-line at source code of the hidden login page.
![nmap-scan](assets/img/brute-it/brute-it-commentline.png)  
This gave the username.

And now we should find the password. For this we will use hydra to brute-force the password.
![nmap-scan](assets/img/brute-it/brute-it-hydra.png)
That wasn't hard. We got the credentials for hidden login page and of course first answer of this task.

Here we are. We captured the Web flag
![nmap-scan](assets/img/brute-it/brute-it-webflag.png)

This is a rsa token for the ssh connection. We are going to use it for authentication.
![nmap-scan](assets/img/brute-it/brute-it-id_rsa.png)

But we have to change the permissions of the id_rsa token.
![nmap-scan](assets/img/brute-it/brute-it-chmod.png)

Let's try to connect.

![nmap-scan](assets/img/brute-it/brute-it-sshtry.png)

---

We need to passphrase to login ssh.
We will use **John** for this.
![nmap-scan](assets/img/brute-it/brute-it-passaphrase.png)

I am trying again.
![nmap-scan](assets/img/brute-it/brute-it-ssh.png)
And now, we are in it.

We captured the user flag.
![nmap-scan](assets/img/brute-it/brute-it-userflag.png)

## Task 4 - Privilege Escallation

For the privilege escalation, i try everytime firstly `sudo -l` .

![nmap-scan](assets/img/brute-it/brute-it-privesc.png)

So we can use `cat` command with root privileges.
read the `/etc/shadows` and `/etc/passwd` for find the password for root
![nmap-scan](assets/img/brute-it/brute-it-shadow.png)

![nmap-scan](assets/img/brute-it/brute-it-passwd.png)

We should unshadowed theese.
![nmap-scan](assets/img/brute-it/brute-it-unshadow.png)

And crack!
![nmap-scan](assets/img/brute-it/brute-it-root.png)

We will use this password to login as root and get the last flag.

Jackpot!
![nmap-scan](assets/img/brute-it/brute-it-rootflag.png)

The **brute-it** room is finished.

## Our achievements in this room:
+ Port Scanning
+ Directory Fuzzing
+ Login Brute-Forcing
+ Password Cracking
+ Privilege Escalation,

I hope it was useful for you.

***Best regards...***

*Carry*



