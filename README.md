# jatinsce21.github.io
To run Three Tier Application using Docker, we need to first create a Full Stack Project. We can use any of our Full Stack Project but if we don’t have one then we can use someone else project also. Here, I have used a very easy simple project on GitLab.This project is made using HTML, CSS, JavaScript, Express and MongoDB.<br>
First you need to clone the Project Repository from the link using command:
git clone https://gitlab.com/nanuchi/developing-with-docker <br>
To run a Three Tier Application, we need to run three Docker Containers simultaneously. So, it is necessary to run all these containers inside a network to avoid their interaction with other containers. 
So, Network can be created by using the following command after starting the Docker Engine with name mongo-network<br>
![Screenshot 2024-04-24 222357](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/96501a87-d3d9-44fd-a067-aac1665d2ab3)
<br>
You can see all the networks using the command: docker network ls. Now, we need to pull the image of MongoDB from DockerHub and make container from it. Then we need to run this container in the network to access MongoDB Database using Docker Container.<br>
![Screenshot 2024-04-24 223028](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/b640e1e6-592d-4317-8253-d7600ec9527b)
<br>
To pull MongoDB image from DockerHub and run it as container we need to execute the command
![Screenshot 2024-04-24 224143](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/02b473fd-1d65-4c64-a4b9-58b2e54f9065)
<br>
Here, the mongo image will be automatically pull from the DockerHub to run the Container in detachable mode with name mongodb in the network mongo-network. The Container will be running on the default 27017 port. You can check all the running containers using command docker ps. Environment Variables Username and Password are also passed to run the container. Similarly, we will be creating another container of Express by pulling its image from the DockerHub.
Express Container can be run by using the follow command
![Screenshot 2024-04-24 224505](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/5bab6b9a-a111-4b8a-a68a-d8c1ac48698e)
<br>
Here, the container with name mongo-express is made to connect the MongoDB Database with the Frontend of the project in Docker. As explained above, the container will run on 8081 port. The environment variables Username and Password are passed of the MongoDB to access the Database along with the container name of the MongoDB in the Server Environment variable. The container will be running on the same network as the above container.
Now, open the link in your browser localhost:8081 and create two databases my-db and user-accounts
![Screenshot 2024-04-24 224927](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/d21b836d-1c9e-4060-b3f1-9dc3d3d44e46)
Creating these two databases is necessary as the Frontend will be requiring these while running. Also, we need to change the MongoDB URL mentioned in the server.js file as we will be running MongoDB using Docker instead of Local Machine.
Naviagate to the server.js file in the project and replace mongoUrlLocal and mongoUrlDocker with the following value
![Screenshot 2024-04-24 225333](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/d3529bf6-c71e-4f99-b74d-e19e7e02b924)
<br>
create a new Dockerfile inside the app folder of the project with the following commands
FROM node WORKDIR /app COPY . . ENV MONGO_DB_USERNAME=admin ENV MONGO_DB_PWD=password RUN npm install EXPOSE 3000 CMD [“node”, “server.js”]<br>
![Screenshot 2024-04-24 225212](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/9a21cb53-85c2-4bb7-9d0c-bd0f6aa4d688)
Open the CMD Terminal inside the app folder of the project and run the command 
![Screenshot 2024-04-24 225732](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/61b6c976-01ed-4849-a65d-4004581f3b08)
To run the Image as a Docker Container run the command
![Screenshot 2024-04-24 230657](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/aa9c0b4f-3de7-4590-8f13-38cf20ae4de6)<br>
Now, open the following link on you browser localhost:3000 and you will see a webpage running.
![Screenshot 2024-04-24 231754](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/8e6fe516-feb9-4bab-a476-08be2d4ca7a2)
To push the Docker Image of the project run the command
![Screenshot 2024-04-24 231754](https://github.com/jatinsce21/jatinsce21.github.io/assets/138685788/e035b57e-f21b-4d6b-931f-0fbc1c357528)
Docker hub repository link : <a href="https://hub.docker.com/repository/docker/mauli573/21bcp079-image/general">https://hub.docker.com/repository/docker/jatinsce21/21bcp436dimage/general</a>
