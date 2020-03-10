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
