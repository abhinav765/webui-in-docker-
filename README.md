# webui-in-docker-

REFER DOCKER IMAGE:- docker pull abhinav766/webui:v1

Webui-hosted-in-Docker

Webpage hosted in Docker using Apache webserver

# Step Should be followed

1. Check docker installed or not systemctl status docker in (Linux base OS) and in windows Run docker version

2. Check if httpd installed or not: systemctl status httpd

3. To check images :- docker images

4. If you dont have any images, pull image from hub.docker.com
   To download/pull image:- docker pull centos:latest

5. To create a container : docker run -it --name "CONTAINER_NAME" centos:latest

 # Step inside the Docker

- Step 1:- rpm -q httpd
- Step 2:- yum install httpd -y
- Step 3:- systemctl start httpd (it fails as systemctl cmds are not directly supported in docker containers)
- Step 4:- To start httpd service : /usr/sbin/httpd (THis will start the httpd service)
- Step 5:- exit
  To make new directory:- mkdir testdir/
  Make one directory inside the "html" directory which will contain all the contents of your webpage
# Create Dockerfile
6. vim Dockerfile

   FROM centos

   RUN yum install httpd -y

   COPY html /var/www/html/

   EXPOSE 80

   CMD /usr/sbin/httpd -DFOREGROUND

 7. docker build -t webui:v1 . ("This will create a image with name 'webui' with version 'v1' ")

 8. docker images ("you will see webui:v1 image")

 9. docker container run -dit -P webui:v1

 # EXPLAINATION
  - EXPOSE 80: It will give you a random port number for your webpage.
    
    We can also give customize port number to our webpage: docker run -dit -p 1234:80 webui:v1 

    This will give your webpage the port number as "1234" Eg-> 172.0.168.105:1234/index.html 

   - View in private network but outside your system: The IP the webpage will the same as of your base OS not the Docker Container IP.
     Eg-> 192.168.0.105:1234/index.html
