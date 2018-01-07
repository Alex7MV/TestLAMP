## Репликация




### Репликация Master -> Slave

#### Права длступа



#### Операции на Master
1. Переводим MySQL-сервер в режим только для чтения данных командами:
~~~
FLUSH TABLES WITH READ LOCK; 
SET GLOBAL read_only = ON;
~~~

2. Выполняем команду см. [документацию](https://dev.mysql.com/doc/refman/5.7/en/show-master-status.html)
~~~
show master status\G;
~~~
Запомним значения File и Position

3. Переносим данные (делаем думп БД, которые мы будем репличировать). Используем пользователя MySQL у которого есть соответстаующие права доступа:
~~~
mysqldump 
    --quote-names 
    --create-options 
    --complete-insert 
    --add-drop-table 
    --order-by-primary 
    --single-transaction 
    --quick -puser_password -uuser_db -hdb_host db_name >db_name.sql
~~~
В итоге получаем файлы вида "db_name.sql", где db_name - название соответстаующей БД.

4. Разрешаем MySQL-серверу вносить изменения в данные:
~~~
UNLOCK tables; 
SET GLOBAL read_only = OFF;
~~~


#### Операции на Slave
