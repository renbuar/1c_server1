# 1c_server1
1 сервер

https://renbuar.blogspot.com/2018/11/docker-1-2-ubuntu-1404.html

$ cd cd ~/  

$ git clone https://github.com/renbuar/1c_server1.git

$ cd ~/1c_server1/

$ cp ~/test/1c-enterprise83-common_8.3.14-1373_amd64.deb ~/1c_server1/

$ cp ~/test/1c-enterprise83-server_8.3.14-1373_amd64.deb ~/1c_server1/

$ cp ~/test/haspd_7.60-eter1ubuntu_amd64.deb ~/1c_server1/

$ cp ~/test/haspd-modules_7.60-eter1ubuntu_amd64.deb ~/1c_server1/

$ docker build --tag 1c-server1 .

Запуск тестовый

$ docker run -ti -h u1604 --name 1c-server-1 --rm  --privileged -p 1540:1540 -p 1541:1541 -p 1560-1591:1560-1591 -p 475:475 -p1947:1947 -v 1c-server1:/home/usr1cv8 1c-server1:latest

 

Запуск разовый

$ docker run -d -h u1604 --name 1c-server-1 --rm  --privileged -p 1540:1540 -p 1541:1541 -p 1560-1591:1560-1591 -p 475:475 -p1947:1947 -v 1c-server1:/home/usr1cv8 1c-server1:latest


Затем создав базу останавливать  :

$ docker stop 1c-server1

При необходимости запускать сноваа:

$ docker start 1c-server1
