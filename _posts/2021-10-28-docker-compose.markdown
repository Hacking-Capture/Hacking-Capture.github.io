---
layout: post
title: Docker-Compose
date: 2021-10-28
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: docker-compose/docker-compose-button.jpg  # Add image post (optional)
tags: [] # add tag
---

Docker Compose is a tool for running multi-container applications on Docker defined using the Compose file format. A Compose file is used to define how the one or more containers that make up your application are configured.

#### Installation on ubuntu 18.04

> sudo apt-get install docker-compose

#### docker-compose version

> docker-compose version

<p>
 <img src="/assets/img/docker-compose/docker-compose-version.png " style="margin-left:2%;" width="449"/>
</p>

#### Starts all stopped containers in the work directory

> docker-compose start

#### Stops all currently running containers in the work directory

> docker-compose stop

#### Validates and shows the configuration

> docker-compose config

#### Lists all running containers in the work directory

> docker-compose ps

#### Stops and removes all containers in the work directory

> docker-compose down

### Configuring WordPress with Compose

> leafpad docker-compose.yml

```
wordpress:
    image: wordpress
    links:
     - mariadb:mysql
    environment:
     - WORDPRESS_DB_PASSWORD=password
     - WORDPRESS_DB_USER=root
    volumes:
     - ./html:/var/www/html
mariadb:
    image: mariadb
    environment:
     - MYSQL_ROOT_PASSWORD=password
     - MYSQL_DATABASE=wordpress
    volumes:
     - ./database:/var/lib/mysql
 
 ```

> docker-compose up -d

#### Check the docker-compose log 

> docker-compose logs

<p>
 <img src="/assets/img/docker-compose/docker-compose-logs.png" style="margin-left:2%;" width="449"/>
</p>

Your WordPress server's public IP address or domain can be viewed in your web browser to check the installation. The WordPress initial setup page should look like the image shown below.

> sudo ifconfig docker0

<p>
 <img src="/assets/img/docker-compose/docker-compose-ip.png" style="margin-left:2%;" width="449"/>
</p>


<p>
 <img src="/assets/img/docker-compose/docker-compose-wordpress.png " style="margin-left:2%;" width="449"/>
</p>

<p>
 <img src="/assets/img/docker-compose/docker-compose-wordpress1.png" style="margin-left:2%;" width="449"/>
</p>

<p>
 <img src="/assets/img/docker-compose/docker-compose-wordpress2.png " style="margin-left:2%;" width="449"/>
</p>
