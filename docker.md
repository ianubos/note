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

```
