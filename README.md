# WpsKali & WPSCAN
Docker Implementation 

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
