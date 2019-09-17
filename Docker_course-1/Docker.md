### Docker For Beginner #########  

# Install docker on amazon linux  
#!/bin/bash    
sudo yum update -y  
sudo yum install -y docker  
sudo service docker start  
sudo usermod -a -G docker ec2-user  
  
log out and log in to pickup the added group   

# now execute  
docker --help  

docker image --help  

docker run hello-world    

docker images  

# just check below command to interactively login to conatiner  
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


## What is conatiner  
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
docker conatiner ls (or) docker ps  
# go to first terminla press ctrl+c  
docker container ls  
docker container ls -a  
docker container rm <Name>  

## how to pass more params to dlete container when it exits  
docker container run -it --rm --name web1 -p 5000:5000 -e FLASK_APP=app.py web1  
docker conatiner ls -a  
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
docker conatiner ls  

# restart docker conatiner automatically  
docker container run -it --rm --name web1_2 -p 5000 -e FLASK_APP=app.py -d --restart on-failure web1  

# restart or rm only one at a time  
docker container run -it --name web1_3 -p 5000 -e FLASK_APP=app.py -d --restart on-failure web1  
docker container ls  
dcoker container stop web1  
dcoker container stop web1_2  

sudo service docker restart  
docker container ls  
##################################  









 






