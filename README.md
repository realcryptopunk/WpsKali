# WpsKali & WPSCAN
Docker Implementation Lab 7 

## Install Docker
- Using the installer at this [link](https://docs.docker.com/docker-for-mac/install/) installs all the components necessary for this exercise.
- Ensure python3 is installed if the usage of modifyCompose CLI app is desired.
- Make sure Docker is running in the background

## Build
Build the image for Kali and make a folder to bind to the Wordpress container

-bash git clone https://github.com/0xrutvij/wpVSkali.git DOCKER_BUILDKIT=1 docker compose build mkdir wpFolder, There is no need to CD into wpFolder
-Cd into wpVSkali
- Build Docker Containers using DOCKER_BUILDKIT=1 docker-compose build
- Create wpFolder as a source for the docker compose, need to use same folder name. 
- Run docker compose to start up containers
- Check the running containers by using docker ps -a

## Wordpress Basics
- Open browser to http://127.0.0.1:8080/ or http://localhost:8080/ or http://0.0.0.0:8080/
-set up wordpress site name using user name and password

##Invoking Kali

-Invoke Kali interactive mode using docker exec -it $CONTAINERID bash
-Make sure you are targetting the correct Wordpress site and use this to pull the name you previously set the wordpress site as.
wget -qO- 'http://127.0.0.1:8080/' | gawk -v IGNORECASE=1 -v RS='</title' 'RT{gsub(/.*<title[^>]*>/,"");print;exit}' 

## WPSCAN

-Create account at wpscan.com and obtain an API TOKEN
-Run a scan and find the vulnerabilities in your site 
-wpscan --url http://127.0.0.1:8080 --api-token YOUR_API_TOKEN

<img src="http://g.recordit.co/ObDimoFIKZ.gif" width=750>

# Assignment 7

Exploits Found: 

1. XSS Vulnerability in Post Edit Page

--adding a script to the title of a post allows us to exploit an XSS vulnerability. 

Steps: 
-Go to posts
-create a new post or edit
- add some script to the title of the post and post it
- navigate to post

<img src="http://g.recordit.co/0kTGV1sT0H.gif" width=750>

2. XSS vulnerability in Page edit

--adding a script to the title of a page allows us to exploit an XSS vulnerability. 

Steps: 
-Go to posts
-create a new page or edit 
- add some script to the title of the post and post it
- Click to view page
<img src="http://g.recordit.co/FZ0y0VBDPP.gif" width=750>

3. XSS Youtube URL embed 

--embeding a script into a Youtube Url allows us to exploit yet another XSS vulnerability.

Steps: 
-Go to posts
-create a new page or edit 
- Use this script to embed an alert within a Youtube URL
- "[embed src='https://youtube.com/embed/457\x3csvg onload=alert(911)\x3e'[/embed]"
- Click to view page
<img src="http://g.recordit.co/8Gv1unKVOq.gif" width=750>
