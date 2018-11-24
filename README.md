# 1c_server1

https://renbuar.blogspot.com/2018/11/docker-1-2-ubuntu-1404.html

$ cd cd ~/  
$ git clone https://github.com/renbuar/1c_server1.git
$ cd ~/1c_server1/
$ cp ~/test/1c-enterprise83-common_8.3.14-1373_amd64.deb ~/1c_server1/
$ cp ~/test/1c-enterprise83-server_8.3.14-1373_amd64.deb ~/1c_server1/
$ cp ~/test/haspd_7.60-eter1ubuntu_amd64.deb ~/1c_server1/
$ cp ~/test/haspd-modules_7.60-eter1ubuntu_amd64.deb ~/1c_server1/

$ docker build --tag 1c-server1 .

Запуск разово
$ docker run -d --name 1c-server1 --rm --net=host --privileged 1c-server1:latest

При каждом создании контейнера нужно пересоздавать  базу.
Что бы не не пересоздавать можно так:

$ docker run -d --name 1c-server1 --net=host --privileged 1c-server1:latest
Затем создав базу останавливать  :

$ docker stop 1c-server1

При необходимости запускать сноваа:

$ docker start 1c-server1
