## Репликация

### Репликация Master -> Slave

#### Права длступа
В целях безопасности лучше создать отдельного пользователя под которым будет выполняться репликация.
См. [привилегии](https://dev.mysql.com/doc/refman/5.7/en/privileges-provided.html)

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
Запомним значения "File" и "Position".

3. Переносим данные из командной строки (делаем думп БД, которые мы будем репличировать). Используем пользователя MySQL у которого есть соответстаующие права доступа:
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
В итоге получаем файлы вида "db_name.sql", где db_name - название соответстаующей БД.

4. Разрешаем MySQL-серверу вносить изменения в данные:
~~~
UNLOCK tables; 
SET GLOBAL read_only = OFF;
~~~

#### Операции на Slave
1. На всякий удаляем остатки от предыдущих репликаций:
~~~
RESET  SLAVE  ALL;
~~~
2. Переносим данные на Slave из командной строки. Можно это делать удаленно или локально, все зависит от размера данных и времени их копирования по сети:
~~~
mysql -u user_db -puser_password -h db_host_slave --database=db_name <db_name.sql
~~~
Можно запустить паралелльно несколько команд на перенос данных, заодно промониторить загрузку процессора, дисковой подсистемы и сети.

3. Делаем очистку логов MySQL-сервера, т.к. нам не нужны логи первичной загрузки данных. Необходимо указать дату и время до которого они будут удалены.
~~~
PURGE BINARY LOGS BEFORE '2017-12-31 13:00:00';
~~~

4. Запскаем репликацию на Slave см. [документацию](https://dev.mysql.com/doc/refman/5.7/en/change-master-to.html). Описываем мастера
~~~
CHANGE MASTER TO
  MASTER_HOST='db_host_master',
  MASTER_USER='user_db_replicator',
  MASTER_PASSWORD='user_db_replicator_password',
  MASTER_LOG_FILE='master_status_file',
  MASTER_LOG_POS=master_status_position,
  MASTER_CONNECT_RETRY=10;
~~~
Непосредственно запеускаем репликацию:
~~~
start slave;
~~~

#### Проверка работоспособности репликации 
Обычно репликация после запуска работает и не требует вмешательства, но из-за технических сбоев (сети, оборудования и т.д.), операций над БД и MySQL-сервером появляются ошибки при выполнении репликации и требуется вмешательство для того чтобы её возобновить.
Статус репликации можно узнать выполнив команду см. [документацию](https://dev.mysql.com/doc/refman/5.7/en/show-slave-status.html)
~~~
show slave status\G;
~~~
- Slave_SQL_Running_State - описание статуса или ошибки репликации.
- Seconds_Behind_Master - количество секунд отставания от Master.

Если в статусе указана команда которую не может выполнить Slave, то ее можно пропустить выполнив:
~~~
SET GLOBAL SQL_SLAVE_SKIP_COUNTER = 1;
~~~
И заново запустить репликацию:
~~~
start slave;
~~~


#### Профилактика 
Для временной остановки репликации можно воспользоваться командой:
~~~
stop slave;
~~~
И заново запустить репликацию после остановки:
~~~
start slave;
~~~
