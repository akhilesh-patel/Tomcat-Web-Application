# Deploy Maven project with docker container on AWS EC2 Machine.

# Step 1: Create ubuntu machine on aws.

# Step 2:  Install docker machine  on ubuntu machine.
           
         apt update

         curl -fsSL https://get.docker.com -o get-docker.sh

         bash get.docker.sh
# Step 3: Clone repository from Github
        apt install git 
        git clone https://github.com/akhilesh-patel/   Tomcat-Web-Application.git

# Step 4: Install Java on ubuntu machine.
          apt update
          sudo apt install default-jdk
          java -version 
# Step 5: Maven install on ubutu machine
         apt install maven 
         mvn -version
# Step 6: build maven Project 
        mvn package
# step 7: After build copy war file 
       cp -r webapp.war /home/ubuntu
# Step 8: Create Docker file
          vim Dockerfile
          FROM tomcat:latest
          COPY ./webapp.war /usr/local/tomcat/webapps/
          RUN cp -r /usr/local/tomcat/webapps.dist/* /usr/local/tomcat/webapps/

# Step 9: Create dockerignorefile
          vim .dockerignore
          DevopsBasics
# Step 10: Create docker image from dockerfile.
       docker build -t tomcat-img .
# Step 11: Create docker container fom own custome image.
       
docker run -it  -p 8080:8080 --name  tomcat-con tomcat-img

# Step 12:  enter public ip into the browser. please  don't forget port number.

http://3.88.168.249:8080/webapp/

# step 12: Remove docker container and docker image.

docker  rm -f $(docker ps -a -q)

docker rmi -f $(docker images -a -q)

# Step 13: Using Docker Compose.
* Install docker-compose 
  
  sudo apt update

  sudo curl -L https://github.com/docker/compose/releases/download/v2.16.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
  
  sudo chmod +x /usr/local/bin/docker-compose

  docker compose version
  
# Step 14: Create docker-compose file.
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
# Steop 15: Run command.
        docker-compose up --build -d
        docker-compose down
        docker-compose up -d
# Step 16 Enter public ip into the browser. please  don't forget port number.
     http://<ip:port>
     http://3.88.168.249:8080/webapp/
     


     








    
    
 













## Authors

- [@Akhilesh Patel](https://www.github.com/akhilesh-patel)




## 🚀 About Me
I'm a Devops Engineer...



## 🔗 Links

[![linkedin](https://img.shields.io/badge/linkedin-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)]( https://www.linkedin.com/in/akhilesh-patel-8983aa1a5/)





## FAQ
* Please feel free to ask me any question you have. I'm here to help and provide information to the best of my abilities










