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

```
#### 2. Run 2 new containers using nginx:alpine image, and attach the net-1 to them
```bash

```
#### 3.  Run another 1 new containers using nginx:alpine image, and attach the net-2 to them
```bash

```
#### 4. Inspect the 3 containers to know their IPs and write them aside
```bash

```
#### 5. Enter a container in the net-1 network and try to ping a container in the net-2 
network (What do you notice?)
```bash

```
#### 6. Enter a container in the net-1 network and try to ping the other container in the 
same network (What do you notice?)
```bash

```
---
## Task 3: Explain the difference between Docker volumes and Bind Mount.
```bash

```


