# Docker-cheat-sheet
Docker cheat sheet
<h3> #System Info</h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
docker --version
docker info
docker  --help
docker -v
</code></pre></div>

<h3> #Service Management </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
sudo service docker start/restart/stop 
</code></pre></div>

<h3> #List Command </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
docker images -a    Image
docker ps -a 
docker container ls -a   Running container
docker volume ls  Volume
docker network ls  Network </code></pre></div>

<h3> #Container Management </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
docker start <container id>
docker stop <container id>
docker stop $(docker ps -a -q)   stop all containers

docker run -d <image name> 

docker logs  <container ID>
docker inspect <container id>

docker exec -it <container id>  /bin/bash

docker run <container id> -e “<ENVIRONEMENT>=<VALUE>”  Pass environment variables
Ex: docker run <container id> -e “SPRING_PROFILES_ACTIVE=dev” -e “server.port=8080”

docker run -d -p 3306:3306 –name mysql-docker-container -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=polling_app -e MYSQL_user=test -e MYSQL_PASSWORD=test123 -v /var/lib/mysql mysql:latest      With Docker Volume

docker run -d -p 3306:3306 –name mysql-docker-container -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=polling_app -e MYSQL_user=test -e MYSQL_PASSWORD=test123 -v mysql:latest      Without Docker Volume </code></pre></div>

<h3> #Publish the Docker Image to Docker Hub </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
Docker login --username=<Docker Hub Username>
Password: <Docker Hub Password>

Docker tag <image id> <docker hub username>/ <Repository Name>
Docker push <docker hub username> / <Repository name> (or) <Repository name>
</code></pre></div>

<h3> #Publish the Docker Image to Docker Hub </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
Docker login --username=<Docker Hub Username>
Password: <Docker Hub Password>

Docker tag <image id> <docker hub username>/ <Repository Name>
Docker push <docker hub username> / <Repository name> (or) <Repository name>
</code></pre></div>

<h3> #Delete Container </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
docker rm <container id>

docker rm $(docker ps -a -q)  Remove stopped container

docker rm $(docker ps -a -f status=exited -q)

docker rm $(docker ps -a -q -f status=exited -f status=created -q)   container removing 
</code></pre></div>

<h3> #Delete Image </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
docker rmi <image id> or docker rmi -f <image id>

docker rmi $(docker images -f dangling=true)   untagged images

docker images -f dangling=true

docker rmi $(docker images -a -l)  All images at one time

docker image prune -a
</code></pre></div>

<h3>#Docker Volumes </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
docker volume prune   Remove all unused volumes

docker volume rm <volume name>   Remove volume name

docker volume rm $( docker volume ls -q --filter  dangling=true)  Remove dangling (untagged) volumes

</code></pre></div>

<h3>#Docker Networking </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
docker network rm <network id>   remove network based id

docker network prune  Remove all unused network

docker network ls |grep “brifge”   Patterns

docker network create –drive bridge <new network name>  Create custom docker bridge network

docker run <container id> -- network <name for network>   Run docker container in a newly created custom bridge network

docker create dev-network  create a custom docker network

docker run -d --network dev-network --name  dev(host) -e MYSQL_user=test -e MYSQL_PASSWORD=test123 -v mysql:latest 
</code></pre></div>


<h3>#Remove all stopped containers, all dangling images and all unused networks </h3>
<div class="snippet-clipboard-content position-relative" data-snippet-clipboard-copy-content="Docker"><pre><code>
docker system prune  
</code></pre></div>
