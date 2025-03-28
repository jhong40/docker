### Docker Play ground
* https://www.katacoda.com/
* https://labs.play-with-docker.com/
- [Common Docker Commands](https://github.com/docker/labs/blob/master/developer-tools/java/chapters/appa-common-commands.adoc)
- [Monitoring Docker Containers](https://github.com/docker/labs/blob/master/developer-tools/java/chapters/ch10-monitoring.adoc)
- [Docker Storage](https://thenewstack.io/methods-dealing-container-storage)

from docker container 2 host:
localhost (host) -> host
localhost (container) -> container
host.docker.internal:

Container: linux kernel space, control group (cgroup), seccomp (allow/deny system call), SELinux

Container run time: runC, cri-o, docker

build tool: buildah, podman, docker
container management tool: docker, podman, kubernetes


# Bridge Network  - default bridge network, user-defined network
- user defined network provide auto DNS resolution btw containers
- container can be attached or detached from the user-defined network on the fly
```
docker network ls  # bridge, host, null
docker network create --driver bridge mybridge  # create mybridge using bridge driver. --driver bridge is the default

docker network create mybridge   # same as above
docker inspect network mybridge  # inspect mybridge network. it has subnet, gateway
docker container run -dt --name mycontainer1 --network mybridge ubuntu  # create ubuntu container in mynetwork
docker container run -dt --name mycontainer2 --network mybridge ubuntu  # create ubuntu container in mynetwork
docker inspect network mybridge  # will show 2 containers with ips in this network
docker exec -it mycontainer1 ping mycontainer2   # will work, not work in default network
``` 
# Host Network  - share the same network with the Host.  
```
docker container run -dt --name mycontainer --network host nginx   # it open the 80 on the host, no -p80:80
```
# None Network
```
docker container run -dt --name mycontainer --network none nginx   # cannot access from anywhere except http://127.0.0.1 on the container
docker exec -it mycontainer bash
  ifconfig # only show lo (local network), no eth
```

















