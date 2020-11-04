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
