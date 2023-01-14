# docker-demo-app

Docker application project 


Step 1
 on your linux server Install Docker 
1.	Set up docker repository

`$ sudo yum install -y yum-utils`



 
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo


2.	Install Docker Engine

$ sudo yum install docker-ce docker-ce-cli containerd.io -y
$ sudo yum install docker*


3.	Start and Enable Docker

$ sudo systemctl start docker
$ sudo systemctl enable docker




4. Run the command below to add your user to run docker commands change the user names if its different from below
$ sudo usermod -aG docker rocky 
$ su - rocky
Logout and login again test if your user can run the following commands 
$ docker ps 


5. Install mongodb 


$ docker pull mongo
$docker pull mongo-express
#we will create a docker network for  the mongodb and mongo-express
$ docker network create mongo-network


6.run the mongo db with some essential environment variables like username and password.run each line of  command below one by one 
$ docker run -d \
   -p 27017:27017 \
   -e MONGO_INITDB_ROOT_USERNAME=admin \
   -e MONGO_INITDB_ROOT_PASSWORD=password \
   --name mongodb \
   --net mongo-network \
   mongo




7.N|B note the name of your mongo container is mongodb
We will run the mongo-express image with some required environment variables as well.

$ docker run -d \
   -p 8085:8081 \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
  -e ME_CONFIG_MONGODB_SERVER=mongodb \
  --net mongo-network \
  --name  mongo-express \
   mongo-express




8.Run docker logs mongo-express to view if our mongo-express ui is working properly
$docker logs mongo-express


#you should see this output


Navigate to your browser http://publicip:8085


You will see this mongo-express dashboard with databases created by default.

Create a new database user-account




In the create database section on the Mongo-express ui >type user 

