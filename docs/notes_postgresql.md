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

Настройка доступа

В файле /var/lib/pgsql/10/data/pg_hba.conf ищем строку:
~~~
# IPv4 local connections:
host    all             all             127.0.0.1/32          ident
~~~
и заменяем её (где 192.168.0.0/24 - подсеть с которй разрешено подключение к БД):
~~~
# IPv4 local connections:
host    all             all             192.168.1.0/24          md5
~~~

В файле /var/lib/pgsql/10/data/postgresql.conf ищем строку:
~~~
#listen_addresses = 'localhost'
~~~
и заменяем на (разрещаем доступ со всех доступных сетевых интерфейсов)
~~~
listen_addresses = '*'
~~~

Настройка фаервола
~~~
sudo firewall-cmd --permanent --add-port=5432/tcp
sudo firewall-cmd --reload
~~~

### [pgAdmin](https://www.pgadmin.org/)
Веб-приложение с открытым кодом, написанное на языке PHP и представляющее собой веб-интерфейс для администрирования СУБД PostgreSQL.

Desktop-версия доступна для скачивания здесь: https://www.pgadmin.org/download/pgadmin-4-windows/ 
