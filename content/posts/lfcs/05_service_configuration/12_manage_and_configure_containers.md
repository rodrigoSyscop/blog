---
title: "12 Manage and Configure Containers"
date: 2019-04-01T16:01:10-03:00
draft: true
---

Containers are all the rage, and it would definitely do you and your resume some good to get some experience under your belt in dealing with them. They enable you to encapsulate your application, dependencies, and data into a single entity that can be easily and quickly transferred, brought up or down, and managed identically on different systems. It really does sound almost too good to be true, so in this lesson, we'll demonstrate using Docker to bring up a web server -- and then completely remove it. This will give you a quick introduction to the exciting world of containers. After this lesson, you'll be able to do some basic Docker commands like download, start, and stop containers. If this whets your interest for more, see our Docker Certification Prep course and our LXD/LXC Deep Dive!

```bash
docker ps

mkdir webstuff/
echo "Hellow from a Docker Container!" > webstuff/index.html

docker run -dit --name webserver -p 80:80 -v $PWD/webstuff/:/usr/local/apache2/htdocs/ httpd:2.4

docker ps

docker stop webserver
docker start webserver

docker stop webserver
docker rm webserver
```