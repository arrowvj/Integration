# Integration

Simple DevOps Project -3
Launch an EC2 instance for Docker host

Install docker on EC2 instance and start services

yum install docker
service docker start
create a new user for Docker management and add him to Docker (default) group
useradd dockeradmin
passwd dockeradmin
usermod -aG docker dockeradmin
Write a Docker file under /opt/docker
mkdir /opt/docker

### vi Dockerfile
# Pull base image 
From tomcat:8-jre8 


# copy war file on to container 
COPY ./webapp.war /usr/local/tomcat/webapps
Login to Jenkins console and add Docker server to execute commands from Jenkins
Manage Jenkins --> Configure system --> Publish over SSH --> add Docker server and credentials

Create Jenkins job

A) Source Code Management
Repository : https://github.com/ValaxyTech/hello-world.git
Branches to build : */master

B) Build Root POM: pom.xml
Goals and options : clean install package

C) send files or execute commands over SSH Name: docker_host
Source files	: webapp/target/*.war Remove prefix	: webapp/target Remote directory	: //opt//docker
Exec command[s]	:

docker stop valaxy_demo;
docker rm -f valaxy_demo;
docker image rm -f valaxy_demo;
cd /opt/docker;
docker build -t valaxy_demo .
D) send files or execute commands over SSH
Name: docker_host
Exec command	: docker run -d --name valaxy_demo -p 8090:8080 valaxy_demo

Login to Docker host and check images and containers. (no images and containers)

Execute Jenkins job

check images and containers again on Docker host. This time an image and container get creates through Jenkins job

Access web application from browser which is running on container

<docker_host_Public_IP>:8090
