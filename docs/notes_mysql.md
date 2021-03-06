## [MySQL](https://www.mysql.com/)

Будем использовать оригинальный дистрибутив [MySQL Community Edition](https://www.mysql.com/products/community/) 
Другие дистрибутивы необходимо выбирать исходя из технической необходимости, функциональности, лицензии и т.д.
~~~
Здесь и далее описывается процесс установки и администрирования MySQL версии 5.7
~~~

### Установка
Официальная страница по скачиванию и установке: https://dev.mysql.com/doc/refman/5.7/en/linux-installation.html

Будем устанавливать MySQL из Yum репозитория, подробный официальный мануал: https://dev.mysql.com/doc/refman/5.7/en/linux-installation-yum-repo.html

После установки **не запускаем** MySQL, т.к. нам его предварительно необходимо настроить.

### Насторойка
В папке /home, создаем папку /mysql, здесь у нас будут располагаться данные mysql.
Чтобы БД имела к ней доступ прописываем права: 
~~~
sudo chown -R mysql:mysql /home/mysql
~~~
Если не отключен **selinux**, то не забываем указать контекст папки, в которой будут храниться данные
~~~
semanage fcontext -a -t mysqld_db_t "/home/mysql(/.*)?"
restorecon -Rv /home/mysql
~~~

Так же не забываем прочитать [2.10.1 Initializing the Data Directory](https://dev.mysql.com/doc/refman/5.7/en/data-directory-initialization.html)

Файл с настройками my.cnf располагается в папке /etc, прописываем папку /home/mysql 
~~~
datadir=/home/mysql
#
# Указываем чтобы все таблицы создавались в нижнем регистре и не учитывася регистр при их написании 
lower_case_table_names=1
#
# Указываем размер буфера для хранения и индексов, и данных
# 70-80% доступной оперативной памяти (если, конечно, используются только InnoDB-таблицы)
#
innodb_buffer_pool_size=128M
~~~

### Запуск /  Автозапуск
При первом не забываем про пароль для пользователя 'root'@'localhost'. 
Он будет автоматически сгененрирован при установке MySQL сервера и для дальнейшего его использования его обязательно необходимо сменить.
Ищем его по строке "A temporary password is generated for root@localhost" в файле /var/log/mysqld.log.

Запуск MySQL 
~~~
sudo service mysqld start
~~~
Проверка статуса MySQL 
~~~
sudo service mysqld status
~~~

Не забаваем что в данной версии в целях безопасности изменились требования к паролям создаваемых пользователей.
Они должны быть не менее 8-ми символов.
Если этот момент был упущен, то лучше еще раз перечитать раздел [2.5.1 Installing MySQL on Linux Using the MySQL Yum Repository](https://dev.mysql.com/doc/refman/5.7/en/linux-installation-yum-repo.html) официальной документации. 

### Администрирование
Подробное описание [администнирования MySQL](notes_mysql_admin.md)

### Перенос данных (содание резервных копий)
Подробное описание [переноса данных](notes_mysql_dump.md)

### Репликация
Подробное описание [репликации MySQL](notes_mysql_replication.md)
