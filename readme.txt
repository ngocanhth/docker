# download image ve may tinh local
# kiem tra image:
 docker images
  docker images --quiet ==> chi xem id
docker pull mcr.microsoft.com/mssql/server:2022-latest

# xoa container

docker rm --force ID_Container

# xoa image

dcoker rmi ID_Image

# docker ps -a

hien tat ca danh sach container dang bat va tat

# Tao ra container tu image

docker run -d image_name

vidu: 

docker run \
-e "ACCEPT_EULA=Y" \
-e "MSSQL_SA_PASSWORD=1988" \
-p 1433:1433 \
-- name mcr.microsoft.com/mssql/server-container-latest \
-d mcr.microsoft.com/mssql/server:2022-latest



-d: Detach(Background) mode
-e: Enviroment
-p: port (anh xa tu loacl vao container tren docker)
--name: container_name
-f: force


docker log container_id

===============

mysql

docker run ^
--name mysql8-container ^
-v mysql8-volume:/var/lib/mysql ^
-e MYSQL_ROOT_PASSWORD=Admin$123 ^
-p 3308:3306 ^
-d mysql

docker run ^
-e MYSQL_ROOT_PASSWORD=Abc@123456789 ^
--name mysql8-container ^
-p 3308:3306 ^
-v mysql8-volume:/var/lib/mysql ^
-d mysql


#  docker compose up -d

docker logs dokcer_name


=============

kiem tra danh sach docker volume:

docker volume ls
docker volume rm -f volume_name
docker volume inspect my_volume_1

===============

Connect Mysql tren container

mysql --protocol=tcp -h localhost -P 3308 -u root -p
Abc@123456789

===========

tao ra network

docker network create docker_network_app

docker network ls

========

nodejs container


docker run -dp 3002:3000 ^
-rm ^
--name todo-app-container ^
-w /app -v "$(pwd):/app" ^
--network todo-app-network ^
-e MYSQL_HOST=todo-app-network-alias ^
-e MYSQL_USER=root ^
-e MYSQL_PASSWORD=Abc@123456789 ^
-e MYSQL_DB=todoDB ^
node ^
sh -c "yarn install && yarn run:dev"
