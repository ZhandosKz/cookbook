# Bash

Объявление переменной с дефолтным значением
```
variable doesn't exist

$ echo "$VAR1"

$ VAR1="${VAR1:-default value}"
$ echo "$VAR1"
default value

variable exists

$ VAR1="has value"
$ echo "$VAR1"
has value

$ VAR1="${VAR1:-default value}"
$ echo "$VAR1"
has value
```

# SSH
### Генерации base64 файла из файла приватного ключа 
```bash
base64 -w 0 id_rsa > id_rsa_64
```
# Docker
### Как сделать named-volume с файлами
```
docker container create --name dummy -v myvolume:/root hello-world
docker cp c:\myfolder\myfile.txt dummy:/root/myfile.txt
docker rm dummy
```
### Запуск временного контейнера
```
docker run --rm -ti -v "$(pwd):/var/www/100hires" image:tag /bin/bash
```

### Как убить контейнеры по имени
```
docker kill $(docker ps | grep selenoid | awk ' {print $1} ')
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

Получение связей таблиц (в примере для таблицы queue)
```mysql
SELECT
    `TABLE_SCHEMA`,                          -- Foreign key schema
    `TABLE_NAME`,                            -- Foreign key table
    `COLUMN_NAME`,                           -- Foreign key column
    `REFERENCED_TABLE_SCHEMA`,               -- Origin key schema
    `REFERENCED_TABLE_NAME`,                 -- Origin key table
    `REFERENCED_COLUMN_NAME`                 -- Origin key column
FROM
    `INFORMATION_SCHEMA`.`KEY_COLUMN_USAGE`  -- Will fail if user don't have privilege
WHERE
        `TABLE_SCHEMA` = SCHEMA()                -- Detect current schema in USE
  AND `REFERENCED_TABLE_NAME` IS NOT NULL and (TABLE_NAME = 'queue' or REFERENCED_TABLE_NAME='queue');
```
