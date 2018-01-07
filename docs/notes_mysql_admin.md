## Администрирование

### БД, создание и удаление
~~~
-- Создаем БД
--
create database db_name;
-- Удаляем БД
--
drop database db_name;
~~~

### Пользователи, права доступа
См. [документацию](https://dev.mysql.com/doc/refman/5.7/en/account-management-sql.html) для детального изучения!!!
~~~
-- Пользователь сможет подключиться к бд только локально (рекомендуется для операций на сервере)
--
CREATE USER 'db_user1'@'localhost' IDENTIFIED BY 'db_user1_pass';

-- Даем все права доступа на все БД пользователю db_user1 подключенного локально
--
GRANT ALL PRIVILEGES ON *.* TO 'db_user1'@'localhost' WITH GRANT OPTION;
~~~


### Обслуживание
Удаляем логи MySQL-сервера до указанной даты - времени с помощью команды:
~~~
PURGE BINARY LOGS BEFORE '2017-12-31 13:00:00';
~~~
