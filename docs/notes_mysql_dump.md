## Перенос данных (содание резервных копий)

Переводим MySQL-сервер в режим только чтение, все изменения и добавления данныз будут дожидаться его окончания или отваливаться по тайсауту: 
~~~
FLUSH TABLES WITH READ LOCK; 
SET GLOBAL read_only = ON;
~~~

Извлекаем данные из БД в файл, выполняем из командной строки (делаем дамп БД, которые мы будем репличировать). Используем пользователя MySQL у которого есть соответстаующие права доступа:
~~~
mysqldump 
    --quote-names 
    --create-options 
    --complete-insert 
    --add-drop-table 
    --order-by-primary 
    --single-transaction 
    --quick -puser_password -uuser_db -hdb_host_master db_name >db_name.sql
~~~

Разрешаем MySQL-серверу вночить изменения в данные и добавлять новые:
~~~
UNLOCK tables; 
SET GLOBAL read_only = OFF;
~~~

Переносим данные из файла в БД, из командной строки. Можно это делать удаленно или локально, все зависит от размера данных и времени их копирования по сети:
~~~
mysql -u user_db -puser_password -h db_host_slave --database=db_name <db_name.sql
~~~
