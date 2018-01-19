## [PostgreSQL](https://www.postgresql.org/)


### Установка
Добавляем yum репозиторий
~~~
sudo rpm -Uvh https://yum.postgresql.org/10/redhat/rhel-7-x86_64/pgdg-centos10-10-2.noarch.rpm
~~~
Устанавливаем
~~~
sudo yum install postgresql10-server postgresql10
~~~
Инициализируем PGDATA
~~~
sudo /usr/pgsql-10/bin/postgresql-10-setup initdb
~~~
Данные будут располагаться по пути /var/lib/pgsql/10/data/

Запуск
~~~
sudo systemctl start postgresql-10.service
sudo systemctl enable postgresql-10.service
~~~

Проверка успешного запуска
~~~
sudo systemctl status postgresql-10.service
~~~

### [pgAdmin](https://www.pgadmin.org/)
Веб-приложение с открытым кодом, написанное на языке PHP и представляющее собой веб-интерфейс для администрирования СУБД PostgreSQL.
