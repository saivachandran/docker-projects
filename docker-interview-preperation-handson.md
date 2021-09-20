docker
======

# configure dockerhub username and password

$ sudo docker login

username: xxx

password: xxx


# pull image from dockerhub

$ sudo docker pull ubuntu


# list docker images

sudo docker image ls

REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
redis        latest    fad0ee7e917a   3 days ago      105MB
ubuntu       latest    7e0aa2d69a15   6 weeks ago     72.7MB
postgres     9.4       ed5a45034282   15 months ago   251MB


# View detail information about docker

$ docker image inspect ubuntu


# view image history

sudo docker image history ubuntu


# remove docker image


sudo docker image rm ubuntu


# push image to docker hub

$ sudo docker commit ceb57cf816f2 chandransaiva/my-repo:test

$ sudo docker push chandransaiva/my-repo:test

$ sudo docker pull chandransaiva/my-repo:test


# save docker image 

sudo docker save 6fdf4d13b0d3 | gzip > postgres.tar.gz

# load docker image 

sudo docker load < postgres.tar.gz

# tag docker image

sudo docker tag 6fdf4d13b0d3 postgres:2



# run docker conatiner using image

sudo docker run -it --name saiva -it 7e0aa2d69a15 bash

# check running container

$ sudo docker ps

# view running and stopped container

sudo docker ps -a

# excute command inside container

sudo docker exec -it ceb57cf816f2 bash

apt update -y


# stop process on container

sudo docker container pause 6fdf4d13b0d3

# start process on container

sudo docker container unpause 6fdf4d13b0d3


# stop,start,restart,kill conatiner


sudo docker container stop 6fdf4d13b0d3

sudo docker container start 6fdf4d13b0d3

sudo docker container restart 6fdf4d13b0d3

sudo docker container kill 6fdf4d13b0d3


# rename conatiner

sudo docker container rename saiva krish


# copy file to container and from container 

sudo docker container cp wsaxis.p12 b1d9bec8d97f:/root/

sudo docker container cp b1d9bec8d97f:/sai.txt .


# start all stopped container

sudo docker start $(docker ps -a -q)
1643e9e260b6
e9633aa2fb61
862dfa821cc2
6fdf4d13b0d3
5eb30dad21c5
ceb57cf816f2


# stop all running container

sudo docker stop $(docker ps -q)
e9633aa2fb61
862dfa821cc2
6fdf4d13b0d3
5eb30dad21c5
ceb57cf816f2


# Display a live stream of container(s) resource usage statistics

sudo docker container stats 1643e9e260b6

# Display the running processes of a container

sudo docker container top 6fdf4d13b0d3


# update command in docker 

sudo docker update --restart=on-failure:3 e9633aa2fb61
e9633aa2fb61


# attach container to monitor 


sudo docker container attach e9633aa2fb61


# docker run command privilleged user

docker run -t -i --privileged ubuntu bash
root@50e3f57e16e6:/# mount -t tmpfs none /mnt

root@50e3f57e16e6:/# df -h
Filesystem      Size  Used Avail Use% Mounted on
none            1.9G     0  1.9G   0% /mnt

07.06.2021
==========

# show difference in container

sudo docker container diff e9633aa2fb61


# docker run commands

sudo docker run -it 7e0aa2d69a15 /bin/bash 
   
sudo docker run -it chandransaiva/my-repo:test bash 
   
 
 
 
sudo docker run -it --name saiva -it 7e0aa2d69a15 bash
 
sudo docker run -d -it --name latest 7e0aa2d69a15 /bin/bash 


sudo docker run -d --name saiva 2e4029753fb0 
  
sudo docker run -d -it --name hassan 2e4029753fb0 
 
docker run hello-world 
      
sudo docker run 2e4029753fb0 /bin/bash   
  
sudo docker run --help  

# run privilleged container    

sudo docker run -i -t 2e4029753fb0 --privileged /mnt  

sudo docker run -i -t 2e4029753fb0 bash   

docker run -i -t --privileged 2e4029753fb0 bash 


# run container with working directory
 
 
sudo docker run -w /opt/ -i -t 2e4029753fb0 pwd 

sudo docker run -w /opt/ -i -t 2e4029753fb0  


# run container with volume

sudo docker run -itd -v /home/master/storage:/opt -w /opt/ 3ef86f7b1163 pwd

sudo docker run -itd -v /home/master/storage:/opt -w /opt/ 3ef86f7b1163 

sudo docker run -itd -v /home/master/storage:/opt -w /opt/ 2e4029753fb0 bash

# Establish port in conatiner

sudo docker run -itd --name port-test -p 80:80 d1a364dc548d bash


# run container with specific port

sudo docker run -itd -p 8080:80 --network=sai d1a364dc548d bash 

sudo docker run -itd -p 8090:80 --network=sai d1a364dc548d bash


Dockerfile
==========

vim Dockerfile

FROM busybox 

ENV sai=/prem

WORKDIR ${sai}

ADD . $sai


#build command

sudo docker build -t test .

# run container from image

sudo docker run -it 1deaebe47b78


# docker file Argument pass

vim Dockerfile

ARG version=latest

FROM busybox:$version
ARG version

RUN echo $version > image_version


#build command

sudo docker build -t argtest .

# run container from image

sudo docker run -it 1deaebe47b78


# excute command inside container without login

sudo docker exec -it hungry_blackwell apt install nginx


# dockerfile throuh stdin 

sudo docker build -t myimage:latest  -f- . <<EOF
FROM busybox
COPY . /
EOF



# build dockerfile with nginx

vim Dockerfile

FROM ubuntu:latest

MAINTAINER Saiva

RUN apt-get update \
    && apt-get install -y nginx \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && echo "daemon off;" >> /etc/nginx/nginx.conf

# forward request and error logs to docker log collector
RUN ln -sf /dev/stdout /var/log/nginx/access.log
RUN ln -sf /dev/stderr /var/log/nginx/error.log

EXPOSE 80 443

VOLUME ["/var/cache/nginx"]

CMD ["nginx", "-g", "daemon off;"]


# sudo docker build -itd --name sai d9d57f8b67ca bash


08.06.2021
==========

# create user in mysql and give remote acesss

CREATE USER 'kavi'@'%' IDENTIFIED BY 'Kavi@*#';

GRANT ALL PRIVILEGES ON *.* TO 'kavi'@'%';

# give user only partcular database

GRANT ALL PRIVILEGES ON database_name.table_name TO 'database_user'@'localhost';

GRANT SELECT, INSERT, DELETE ON database_name.* TO database_user@'localhost';

flush privileges


docker-compose
-------------

vim docker-compose.yml

version: "3.1"
networks:
  saiva:
services:
  web:      
     image: nginx
     volumes: 
       - webdata:/usr/share/nginx/html
     ports:
       - "8090:80"
     environment:
       - NGINX_HOST=web.saiva.com
       - NGINX_PORTi=80
     restart: always         
     networks:
       - saiva      
  db:
    image: mysql:5.7
    container_name: db
    environment:
      MYSQL_ROOT_PASSWORD: Saiva@*#
      MYSQL_DATABASE: app_db
      MYSQL_USER: saiva
      MYSQL_PASSWORD: Saiva@*#
    restart: always  
    ports:
      - "3306:3306"
    volumes:
      - dbdata:/var/lib/mysql
    networks:
      - saiva      
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: pma
    links:
      - db
    environment:
      PMA_HOST: db
      PMA_PORT: 3306
      PMA_ARBITRARY: 1
    restart: always
    ports:
      - 8081:80
    networks:
      - saiva      
volumes:
  dbdata:
  webdata: 


# validate docker-compose file

sudo docker-compose.yml config


# run docker-compose file

sudo docker-compose up -d


# backup database inside the mysql conatiner

sudo docker exec db /usr/bin/mysqldump -u kavi --password=Kavi@*# --all-databases > backup.sql

# restore mysql database inside the container

cat backupsai.sql | docker exec -i db /usr/bin/mysql -u kavi --password=Kavi@*# 


Create and manage volumes
=========================

# create volume 

 sudo docker volume create saiva-volume

# list created volume

   sudo docker volume ls

# inspect volume

sudo docker volume inspect saiva-volume


# run conatiner with volume


sudo docker run -itd --name volume-test --mount source=saiva-volume,target=/app 7e0aa2d69a15 bash




create network 
==============

# create network 

sudo docker network create -d bridge sainetwork


# view created network 

sudo docker network ls

# inspect docker network 

sudo docker network inspect sainetwork

# run conatiner to specific network

sudo docker run -itd --net=sainetwork --name dfg 7e0aa2d69a15 bash

# get container ip address


11.06.2021
========

centos with systemd
-------------------

vim Dockerfile

FROM centos/systemd

MAINTAINER "Your Name" <you@example.com>

RUN yum -y install httpd; yum clean all; systemctl enable httpd.service

EXPOSE 80

CMD ["/usr/sbin/init"]


docker build --rm --no-cache -t httpd .


docker run --privileged --name httpd -v /sys/fs/cgroup:/sys/fs/cgroup:ro -p 80:80 -d  httpd



12.06.2021
---------

# remove all stopeed conatiner and unused images 

$ sudo docker system prune


# we can json file instead of yaml file 

docker-compose -f docker-compose.json up


## docker example1
------------------


Dockerfile

FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get install -y apache2  php   openssl   php-common php-mbstring  php-xml php-mysqlnd php-gd  php-pdo php-curl  vim  && apt-get clean
RUN sed -i 's/max_execution_time = 30/max_execution_time = 1500/g' /etc/php/7.4/apache2/php.ini
RUN ln -sf /dev/stdout /var/log/apache2/access_log \
&& ln -sf /dev/stderr /var/log/apache2/error_log
EXPOSE 80 443
CMD ["apachectl", "-D", "FOREGROUND"]


## build docker file

docker build -t saiva/test:v1 .



cat docker-compose.yml 

version: '3.2'
networks:
 saiaxis:
services:
  web:
    container_name: sai-api-server
    hostname: sai-api-server
    image: saiva/test:v1
    restart: unless-stopped
    ports:
      - "8080:80"
    volumes:
      - /webdata/sai:/var/www/html
    networks:
      - saiaxis
 

## validate docker-compose file

docker-compose -f docker-compose.yml config

networks:
  saiaxis: {}
services:
  web:
    container_name: sai-api-server
    hostname: sai-api-server
    image: saiva/test:v1
    networks:
      saiaxis: null
    ports:
    - published: 8080
      target: 80
    restart: unless-stopped
    volumes:
    - /webdata/sai:/var/www/html:rw
version: '3.2'

# up docker-compose file after validating

docker-compose up -d


# down docker-compose file

docker-compose down


#centos dockerfile

cat Dockerfile 

FROM centos:7
RUN yum install -y httpd mod_ssl openssl php php-common php-mbstring  php-xml php-mysqlnd php-gd php-mcrypt php-pdo mysql wget curl cronie vim
COPY keys/wq.crt /etc/pki/tls/certs/
COPY keys/wq.key /etc/pki/tls/certs/
COPY keys/ca-bundle-client.crt /etc/pki/tls/certs/
COPY conf/vhost.conf /etc/httpd/conf.d/wsaxis.wq.conf
COPY conf/vhost-ssl.conf /etc/httpd/conf.d/sai.wq.ssl.conf
COPY conf/security.conf /etc/httpd/conf.d/
ADD conf/index.php /var/www/html/
RUN ln -sf /dev/stdout /var/log/httpd/ssl_access_log \
&& ln -sf /dev/stderr /var/log/httpd/ssl_error_log   \
&& ln -sf /dev/stdout /var/log/httpd/access_log      \
&& ln -sf /dev/stderr /var/log/httpd/error_log \
&& ln -sf /dev/stderr /var/log/httpd/ssl_wsaxis_error_log
EXPOSE 80 443
CMD ["httpd", "-D", "FOREGROUND"] 

# docker build command

docker build -t saicentos/test:v1 .


cat docker-compose.yml 
version: '3.2'
networks:
  sai:

services:
  web:
    image:  saicentos/test:v1
    restart: unless-stopped
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /backup/docker/webdata/wsaxis:/var/www/html
    networks:
      - wsaxis
  mysql:
    image: mysql:5.7
    environment:
      - MYSQL_ROOT_PASSWORD=8AA67zn44XpyVZ9b
      - MYSQL_PORT=3306
      - MYSQL_DATABASE=rcms_test
      - MYSQL_USER=sqladmin
      - MYSQL_PASSWORD=9Qf2+kXrM@h9ZNhnL{Qnf
      - MYSQL_LOWER_CASE_TABLE_NAMES=0
    restart: unless-stopped
    volumes:
      - mysql_data:/var/lib/mysql
      - /backup/docker/mysql_backup:/mnt
    networks:
      - sai
volumes:
  mysql_data:


# docker file validation 

docker-compose -f docker-compose.yml config

# docker-compose up command

docker-compose up -d

docker-compose down

===============================================================================================


# run a new conatiner from image

$ docker run -itd nginx

# Assign name to container

$ docker run -itd  --name web nginx

0e046568c2cf82c84ed679679de70522c120957c510751860201f5e220c5de62

# assign port to container

$ docker run -itd --name web -p 80:80 nginx

a7b5364146856652cc45dd2e7d5270bb609b9fee29ac9469df78e843b33a8919

# Assign hostname to conatiner

$ docker run -d --name web -p 80:80 --hostname saiva.com nginx

cd5191ccacf3410970916294fa0a058dc4fe9e8b2a97c85d64ba7154366641ae

# map the localdirectory into container

docker run -d --name web -p 80:80  -v ~/:/usr/share/nginx/html nginx

# change entrypoint of container

docker run -itd --entrypoint bash nginx

# show the list of running conatiner

$ docker ps

# show list of all conatiner

$ docker ps -a

# delete stopped container

$ docker rm web

# delete running conatiner

$ docker rm -f 92d1242237e8

# copy file from conatiner to host system

$ docker cp myubuntu:/index.html  index.html


# copy file from host to conatiner

$ docker cp index.php myubuntu:/index.php

# rename docker conatiner

$ docker rename myubuntu saiubuntu


# commit the running conatiner

$ docker commit saiubuntu 

sha256:519f8c5857f9885d6dc545a31ad50cc9c60b3e1391079f8dc5ad80b9ce8783f6

# tag docker image

$ docker tag 519f8c5857f9 newubuntu/new:v1

# view mapped port in docker conatiner

$ docker port 390589182af3

80/tcp -> 0.0.0.0:80
80/tcp -> :::80

# show the docker process 

$ docker top 390589182af3

# show stats of docker conatiner

$ docker stats 390589182af3

CONTAINER ID   NAME                 CPU %     MEM USAGE / LIMIT     MEM %     NET I/O         BLOCK I/O     PIDS
390589182af3   friendly_matsumoto   0.00%     2.605MiB / 1.933GiB   0.13%     1.18kB / 142B   0B / 8.19kB   3

# inspect docker conatiner

$ docker inspect 390589182af3

# search dockerhub officeal images

$ docker search centos


# github refrence links

https://github.com/wsargent/docker-cheat-sheet

https://dockerlabs.collabnix.com/docker/cheatsheet/

 




















































