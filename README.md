# ITI - Docker Lab2 🐋

## Task 1:
Run a container using nginx image, and mount a directory from your host into the 
Docker container. example: /home/samy/nginx:/home/nginx (bind mount)
```bash
1) Create a Bind Mount directory 
mkdir nginx_bindMount
cd nginx_bindMount/
touch test.txt

2) Run a container using nginx image
docker run -d --name nginx_bindMount -v /root/nginx_bindMount:/usr/share/nginx/html nginx-ahmed

3)check if the file is mounted on the machine
docker exec -it nginx_bindMount bash
cd /usr/share/nginx/html/
ls
the test.txt exists means that it is mounted into the container
```
---

## Task 2:
### Steps
#### 1. Create 2 docker network (net-1 & net-2)
```bash
docker network create network_1
docker network create network_2
```
#### 2. Run 2 new containers using nginx:alpine image, and attach the net-1 to them
```bash
docker run -d --name nginx_net1 --net network_1 nginx:alpine
docker run -d --name nginx_net2 --network network_1 nginx:alpine
```
#### 3.  Run another 1 new containers using nginx:alpine image, and attach the net-2 to them
```bash
docker run -d --name nginx_net3 --net network_2 nginx:alpine
```
#### 4. Inspect the 3 containers to know their IPs and write them aside
```bash
docker inspect -f '{{.NetworkSettings.Networks.network_1.IPAddress}}' nginx_net1
172.18.0.2
docker inspect -f '{{.NetworkSettings.Networks.network_1.IPAddress}}' nginx_net2
172.18.0.3
docker inspect -f '{{.NetworkSettings.Networks.network_2.IPAddress}}' nginx_net3
172.20.0.2
```
#### 5. Enter a container in the net-1 network and try to ping a container in the net-2 
network (What do you notice?)
```bash
docker exec -it nginx_net1 sh 
ping 172.20.0.2
ping fails
```
#### 6. Enter a container in the net-1 network and try to ping the other container in the 
same network (What do you notice?)
```bash
docker exec -it nginx_net1 sh 
ping 172.18.0.2
ping 172.18.0.3
ping successful
```
---
## Task 3: Explain the difference between Docker volumes and Bind Mount.
```bash
Docker Volumes
- It is stored within a directory on the Docker host.
- Managed by Docker and are isolated from the core functionality of the host machine.
- Docker volumes can be named and managed independently of containers
- Can be mounted into multiple containers simultaneously.
- Deleting a container does not delete the volume.

Docker Bind Mounts
- Bind mounts have limited functionality compared to volumes.
- Bind mounts are linked to a specific directory or file on the Docker host filesystem.
- The file or directory is referenced by its full path on the host machine.
- When you use a bind mount, a file or directory on the host is mounted into the container, and allowing the container to access the host's filesystem.
- You can’t use Docker CLI commands to directly manage bind mounts.
```


