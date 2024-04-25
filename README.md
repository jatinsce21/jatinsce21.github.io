# jatinsce21.github.io
To run Three Tier Application using Docker, we need to first create a Full Stack Project. We can use any of our Full Stack Project but if we don’t have one then we can use someone else project also. Here, I have used a very easy simple project on GitLab.This project is made using HTML, CSS, JavaScript, Express and MongoDB.<br>
First you need to clone the Project Repository from the link using command:
git clone https://gitlab.com/nanuchi/developing-with-docker <br>
To run a Three Tier Application, we need to run three Docker Containers simultaneously. So, it is necessary to run all these containers inside a network to avoid their interaction with other containers. 
So, Network can be created by using the following command after starting the Docker Engine with name mongo-network<br>
![1](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/e1ef96ad-4694-44b8-a2f4-6d8358b1a80a)
<br>
You can see all the networks using the command: docker network ls. Now, we need to pull the image of MongoDB from DockerHub and make container from it. Then we need to run this container in the network to access MongoDB Database using Docker Container.<br>
![2](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/234620bc-3194-475f-9b01-c543b6c57c28)
<br>
To pull MongoDB image from DockerHub and run it as container we need to execute the command
![4](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/8ebc6ec9-c9c6-4f92-9caa-d06e71a3b057)
<br>
Here, the mongo image will be automatically pull from the DockerHub to run the Container in detachable mode with name mongodb in the network mongo-network. The Container will be running on the default 27017 port. You can check all the running containers using command docker ps. Environment Variables Username and Password are also passed to run the container. Similarly, we will be creating another container of Express by pulling its image from the DockerHub.
Express Container can be run by using the follow command
![5](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/7dcf1da5-4cf5-47a4-b198-97145b29eff6)
<br>
Here, the container with name mongo-express is made to connect the MongoDB Database with the Frontend of the project in Docker. As explained above, the container will run on 8081 port. The environment variables Username and Password are passed of the MongoDB to access the Database along with the container name of the MongoDB in the Server Environment variable. The container will be running on the same network as the above container.
Now, open the link in your browser localhost:8081 and create two databases my-db and user-accounts
![8](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/0e43593b-0c92-4464-9d04-053134701322) <br>
Creating these two databases is necessary as the Frontend will be requiring these while running. Also, we need to change the MongoDB URL mentioned in the server.js file as we will be running MongoDB using Docker instead of Local Machine.
Naviagate to the server.js file in the project and replace mongoUrlLocal and mongoUrlDocker with the following value
![3](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/c3e788f2-5ef4-428d-8b07-be9842bf2851)
<br>
create a new Dockerfile inside the app folder of the project with the following commands
FROM node WORKDIR /app COPY . . ENV MONGO_DB_USERNAME=admin ENV MONGO_DB_PWD=password RUN npm install EXPOSE 3000 CMD [“node”, “server.js”]<br>
![9](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/beff157e-f9fa-4983-8bbd-3f4471119f84) <br>
Open the CMD Terminal inside the app folder of the project and run the command 
![11](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/b9cdf485-3d30-4b2c-a6cb-3a4704c2acb6) <br>
To run the Image as a Docker Container run the command
![12](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/5ea0555f-1a95-4a5a-a145-a23b854afe01)
![6](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/a08c83b2-1d2e-4c8b-b0d7-440e15ad3859) <br>
Now, open the following link on you browser localhost:3000 and you will see a webpage running.
![14](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/52267411-1d7a-4c17-a116-fddfed26d5f9)<br>
To push the Docker Image of the project run the command
![13](https://github.com/jatinsce21/21BCP436D.github.io/assets/138685788/d251b7f0-d242-4422-9681-90519296fe60) <br>
