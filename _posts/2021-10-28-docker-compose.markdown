---
layout: post
title: wordpress with Docker-Compose
date: 2021-10-28
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: docker-compose/wordpress-docker-compose.png   # Add image post (optional)
tags: [] # add tag
---

<p align="center">
 <img src="/assets/img/docker-compose/wordpress-docker-compose.png" style="margin-left:2%;" width="449"/>
</p>


Docker Compose is a tool for running multi-container applications on Docker defined using the Compose file format. A Compose file is used to define how the one or more containers that make up your application are configured.

#### Installation on ubuntu 18.04

> sudo apt-get install docker-compose

#### docker-compose version

> docker-compose version

<p>
 <img src="/assets/img/docker-compose/docker-compose-version.png" style="margin-left:2%;" width="449"/>
</p>

#### Starts all containers in the working directory that have been stopped

> docker-compose start

#### Stops all running containers in the current directory

> docker-compose stop

#### Validates and displays configuration

> docker-compose config

####  Lists all containers running in the working directory

> docker-compose ps

#### This command stops and removes all containers in the working directory

> docker-compose down

### Configuring WordPress with Compose
create a wordpress-compose and navigate to it.

> mkdir wordpress-compose && cd wordpress-compose

Setting up containers with Docker Compose works by creating a Dockerfile and docker-compose.yml in the desired working directory

create a docker-compose.yml file. This will tell docker how to configure and start the WordPress and MariaDB containers.

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

Using the command below, create new containers. This starts both containers in the background and leaves them running. If you wish to see the output from the containers just leave out the -d to deploy the applications in the foreground.

> docker-compose up -d
> 
> -d running in foreground

You need to wait until the installation is complete. Once the process is complete, you'll see something similar to the example output below.

<p>
 <img src="/assets/img/docker-compose/docker-compose-created.png" style="margin-left:2%;" width="449"/>
</p>

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
