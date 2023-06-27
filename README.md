#########Deploy Maven project with docker container on AWS EC2 Machine. ###########

step 1: create ubuntu machine on aws



Step 2:  Install docker on ubuntu machine


apt update

curl -fsSL https://get.docker.com -o get-docker.sh

bash get.docker.sh


step 3: Clone repo from GitHUb 


apt install git // i think already installed


git clone <url>


step 4: Install Java on ubuntu machine


apt update

sudo apt install default-jdk

java -version 


step 5: Maven install on ubutu machine


apt install maven 

mvn -version


step 6: build java application


mvn package


step 7: After build copy war file 


cp -r webapp.war /home/ubuntu



step 8: Create Dockerfile



vim Dockerfile


FROM tomcat:latest

COPY /home/ubuntu/webapp.war /usr/local/tomcat/webapps/

RUN cp -r /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps/


step 9: Create dockerignorefile


vim .dockerignore 


DevopsBasics // projectname 


 
step 10: Create docker image from dockerfile

docker build -t tomcat-img .


step 11: Create docker container fom own custome image.


docker run -it  -p 8080:8080 --name  tomcat-con tomcat-img


step 11: enter public ip into the browser. please  don't forget port number.


http://3.88.168.249:8080/webapp/

step 12: Remove docker container and docker image.


docker  rm -f $(docker ps -a -q)

docker rmi -f $(docker images -a -q)


#########docker-compose file###############


step 12: Install docker-compose 

sudo apt update

sudo curl -L https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker compose version


step 13: Create docker-compose file.


vim docker-compose.yml

 
version: '3'
services:
  tomcat:
    build:
       context: .
       dockerfile: Dockerfile
    image: tomcat-img
    container_name: tomcat-con
    restart: always
	ports:
      - '8080:8080'
	  
step 14: Run commands 

docker-compose up --build -d

docker-compose down

docker-compose up -d


step 15: enter public ip into the browser. please  don't forget port number.

http://3.88.168.249:8080/webapp/

step 16: delete ubuntu machine 


