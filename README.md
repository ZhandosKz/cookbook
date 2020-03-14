# Docker
### Как сделать named-volume с файлами
```
docker container create --name dummy -v myvolume:/root hello-world
docker cp c:\myfolder\myfile.txt dummy:/root/myfile.txt
docker rm dummy
```

# Mysql

Получение списка юзеров
```mysql
select * FROM mysql.user\G
```

Создание юзера
```mysql
CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';
```

Создание БД и ассайн юзера
```mysql
CREATE DATABASE my_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
GRANT ALL PRIVILEGES ON * . * TO 'zhandos'@'localhost';
```
