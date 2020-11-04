# Docker
By [Travesy Media](https://www.youtube.com/watch?v=Kyx2PsuwomE&t=463s)

## Docker commands
```
docker container run -it -p 80:80 nginx
// -it -> interactive mode flag
// -p -> --publish
// 80:80 -> <local machine port(nginx default is 80)>:<exposed container(apach is 80)>
```
nginx etc... image are came from [hub.docker.com](https://hub.docker.com/). Check it.
There are bunch of information.
Docker has automatically pulled image "docker pull nginx".

```
docker container ls // Show running containers -> "docker ps" is same command!
docker container ls -a // All of the containers -> "docker ps -a" is same!
docker container rm <container id>  // Remove container
docker images // Show images, even if container has been deleted, there is still image
docker image rm <image id> // Remove image
docker pull <image name> // Pull the image

docker container run -d -p 8080:80 --name mynginx nginx
// -d -> detouched, running on background
// --name <name> -> Give the container a name
// nginx -> last term mentioned the image you want to pull

docker container run -d -p 8081:80 myapache httpd
docker container run -d -p 3306:3306 --name mysql --env MYSQL_ROOT_PASSWORD=123456 mysql

docker container stop <container name> // Stop container running
docker container rm myapache // Running container cannot be removed.
docker container rm myapache -f // -f flag is force to do

docker container exec -it mynginx bash // Interactive mode into container inside
#cd usr/share/nginx/html  // There is a html file showing up in the localhost.
#exit

docker rm $(docker ps -aq) -f  // Remove all the container at all

docker container run -d -p 8080:80 -v C:/(pwd):/usr/share/nginx/html --name nginx-website nginx
// -v mount html folder with local folder where you are
```

Inside the test directory...
TEST
|-about.html
|-index.html
|-Dockerfile

DockerFile
```
FROM nginx:latest

WORKDIR /usr/share/nginx/html

COPY . .
```

docker commands
```
docker image build -t <image name you create>  // Make image this time "btraversy/nginix-website"
// -t -> name image
docker rm nginx-website -f

docker container run -d -p 8082:80 btravesy/nginx-website
// localhost:8082 shows index.html!

docker push btravesy/nginx-website // Push the image to Docker Hub like Github!

```

# Dokcer practice with Node&MongoDB
By [Travesy Media](https://www.youtube.com/watch?v=hP77Rua1E0c&t=5s)

DockerFile
```
FROM node:10

WORKDIR /usr/src/app

COPY package*.json ./    # package.json and package-lock.json

RUN npm install

COPY . .

EXPOSE 3000     # app uses this port

CMD ["npm", "start"]     # Run command to start server
```
docker-compose.yml
```docker
version: '3'
services:
  app:
    container_name: docker-node-mongo
    restart: always
    build: .
    ports:
      - '80:3000'       #app uses 3000 port
    external_links:
      - mongo           # chain the mongo and app container
  mongo:
    container_name: mongo
    image: mongo
    ports:
      - '27017:27017'   # MongoDB uses this port

```
