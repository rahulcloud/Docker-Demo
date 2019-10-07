### Docker For Beginner #########  

# Install docker on amazon linux  
#!/bin/bash   
sudo yum update -y  
sudo yum install -y docker  
sudo service docker start  
sudo usermod -a -G docker ec2-user  
  
# log out and log in to pickup the added group   

# now execute  
docker --help  

docker image --help  

docker run hello-world    

docker images  

# just check below command to interactively login to container  
docker run -it alpine sh  

# to check the above list out the file system  
ls -la  
cd home  
touch file.txt  
ls -la  
exit  
#############
# Now re Run the Above command  
docker run -it alpine sh  
ls -la home  

#############################################  
## Now Lets try writing our own Dockerfile  

checkout github repo of docker-demo  
start writing dockerfile and understand some docker comamnds  

docker --help  
docker image --help  
# start building our dockerfile  
make sure you have cloned all repo dependency files and run below command  
# docker image build  -t web1 .  
check the output log  
## FYI- try re-Running above command to check the output  
now docker cached in action  
Now edit maintained tag and re run above  

## It's Time to inspect the dokcer image now  
docker image inspect web1  
now execute below command to add a tag  
# docker image build  -t web1:1.0 .  
# now check images created by docker  
docker image ls  
# how to delete docker image  
docker image rm web1:1.0  
docker image ls  


## What is container  
# How to make docker image as container  
docker container ls  
      OR  
docker ps  
# docker container run -it -p 5000:5000 -e FLASK_APP=app.py web1  
goto browser and try below  
http://localhost:5000  
if using docker toolbox  
http://192.168.99.100:5000  
docker-machine ip  

# open a new terminal and try below  
docker container ls (or) docker ps  
# go to first terminla press ctrl+c  
docker container ls  
docker container ls -a  
docker container rm <Name>  

## how to pass more params to dlete container when it exits  
docker container run -it --rm --name web1 -p 5000:5000 -e FLASK_APP=app.py web1  
docker container ls -a  
## Run container in the background  
docker container run -it --rm --name web1 -p 5000:5000 -e FLASK_APP=app.py -d web1  
docker container ls  
## check the docker container logs  
docker container logs web1<Name or ID>  
or  
docker logs ContainerName/ContainerID  
refresh webpage and check logs  
or  
docker container logs -f web1<Name or ID>  
or  
docker logs -f ContainerName/ContainerID  
# check stats --optional  
docker container stats  

##some juggling with docker commands  
make another copy of existing container  
docker container run -it --rm --name web1 -p 5000:5000 -e FLASK_APP=app.py -d web1  

# ports bind error to resolve  
docker container run -it --rm --name web1_2 -p 5000 -e FLASK_APP=app.py -d web1  
docker container ls  

# restart docker container automatically  
docker container run -it --rm --name web1_2 -p 5000 -e FLASK_APP=app.py -d --restart on-failure web1  

# restart or rm only one at a time  
docker container run -it --name web1_3 -p 5000 -e FLASK_APP=app.py -d --restart on-failure web1  
docker container ls  
dcoker container stop web1  
dcoker container stop web1_2  

sudo service docker restart  
docker container ls  
##################################  
## Volumes?? 

Now lets see about some code chnages effects  
docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 web1  
browser  
Edit app.py file and chnage return value 0 to something else  

browser  
Ctrl+c  
docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 web1  
Edit app.py file and chnage return value 0 to something else  

Ctrl+c  
docker image build -t web1 .  
docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 web1  
Now Browser show changed items  
########################################  
# Adding Volumes tags  

docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v $PWD:/app web1  

we can inspcect this  
open new terminal window  
docker container inspcect web1  
goto mounts section to check bind mount point  
Goto Browser and check  

#######################################  

## if required chnage below  
FROM python:2.7-alpine  
      to  
FROM python:2.7-slim  

docker image build -t web1 .  
#######################  
# connecting to Running containers  
docker container run -it -p 5000:5000 -e FLASK_APP=app.py --rm --name web1 -e FLASK_DEBUG=1 -v $PWD:/app web1  

docker container exec -it web1 bash  

###################################  

# tag docker image  
docker tag <CONT-ID> drahulgandhi/docker-40:flaskapp1  
  
docker login  

docker push `<Docker-Username>/<Repo-Name>`:CONTTag  


docker cp `./webapp.war demo:/usr/local/tomcat/webapps`  

# Linking containers with Docker networks  

###################################  
# create a new image from Docker Course-2  

docker image build -t web2 .

Now we deal with two images to connect to a network pull down a redis image  
docker pull redis:3.2-alpine  
# Note: `in order to communicate between two systems first they should be in same network this is basic idea`  
![Networking](https://github.com/rahulcloud/Docker-Demo/blob/master/images/network-1.PNG)  
![Networking](https://github.com/rahulcloud/Docker-Demo/blob/master/images/network-2.PNG)  
![Networking](https://github.com/rahulcloud/Docker-Demo/blob/master/images/network-3.PNG)  
Two types of networks:  
internal:LAN  
External:WAN  


