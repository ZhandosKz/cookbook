# Google Workspace Addons

## Refs 

- ui kit https://www.figma.com/community/file/848275628252039675
- scopes https://developers.google.com/workspace/add-ons/concepts/gsuite-scopes
- github gmail addon example https://github.com/googleworkspace/add-ons-samples/tree/42d1059ed850003b0de2b859ffd853c2173fa6cc/github
- cats gmail/docs addon example https://developers.google.com/workspace/add-ons/cats-quickstart
- gmail app script api https://developers.google.com/apps-script/reference/gmail
- message.getFrom() bug https://stackoverflow.com/questions/59449863/gmail-appscript-mailmessage-getfrom-to-return-email-not-name
 
# Google App scripts

## Установка clasp для локальной разработки

- удаляем старую ноду `sudo apt purge nodejs npm`
- ставим nvm `curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh | bash`
- перезапускаем терминал и устанавливаем последнею версию ноды nvm install node
- ставим глобально библиотеку для менеджмента скриптов google app script `sudo npm -g install @google/clasp`
- авторизуемся в clasp `clasp login`

# Certbot

### Зарегать сертфикаты для доменов без участия nginx сервера

`sudo certbot certonly --webroot-path путь-до-открытой-вебу-папки --expand -d example.com -d www.example.com -d subdomain.example.com`

# Linux
### Поиск всех ссылок
`find -L /var/www/ -xtype l`

# Elasticsearch

### Delete index
`curl -XDELETE localhost:9200/test_index`

### Create index
`curl -XPUT localhost:9200/test_index`

### Close and open index before change index settings
* `curl -XPOST localhost:9200/test_index/_close`
* `curl -XPOST localhost:9200/test_index/_open`

### Change index settings (sometimes need close index before)
`curl -XPUT localhost:9200/test_index/_settings`

### Change index mappings
`curl -XPUT localhost:9200/test_index/_mapping`

### Test built-in analyzers
```
curl -XPOST -H "Content-Type: application/json" localhost:9200/_analyze?pretty -d'
{
  "analyzer": "english",
  "text":     "Kauffman The quick brown fox."
}'
```

### Test index analyzers
```
curl -XPOST -H "Content-Type: application/json" localhost:9200/test_index/_analyze?pretty -d'
{
  "analyzer": "autocomplete",
  "text":     "Kauffman The quick brown fox."
}'
```



# Bash
### Объявление переменной с дефолтным значением
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

### Присвоение переменной результата логического выражения
``` bash
export test_cond_var1='master'
export test_cond_var2='1'
```
***
Проверка на ИЛИ
``` bash
export test_cond_var3=$(expr "$test_cond_var1" == "master" "|" "$test_cond_var2" == "2")
echo $test_cond_var3
```
Выведет 1, т.к. условие `test_cond_var1=='master'` верное
``` bash
export test_cond_var3=$(expr "$test_cond_var1" == "mas" "|" "$test_cond_var2" == "2")
echo $test_cond_var3
```
Выведет 0, т.к. ни одно из условий не истино 
***
Проверка на И
``` bash
export test_cond_var3=$(expr "$test_cond_var1" == "master" "&" "$test_cond_var2" == "2")
echo $test_cond_var3
```
Выведет 0, т.к. одно условий не истино
``` bash
export test_cond_var3=$(expr "$test_cond_var1" == "master" "&" "$test_cond_var2" == "1")
echo $test_cond_var3
```
Выведет 1, т.к. все условия истины

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
docker run --rm -ti -v "$(pwd):/var/www" image:tag /bin/bash
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
