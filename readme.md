项目运行需要的服务

基于docker容器运行的php-fpm

docker create network my_network

启动：执行 docker-compose up -d --build

docker compose up -d --build php73

docker compose up -d --force-recreate nginx


临时切到root运行
docker compose exec -u root php73 /bin/bash

docker exec -it -u root x-php73 bash