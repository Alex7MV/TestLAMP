## [Oracle Database](https://www.oracle.com/database/index.html)
[Oracle 11g Express Edition Database](http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html) для скачивания и бесплатного использования.


1. Скачиваем дистрибутив по ссылке выше.
На текущий сосент это файл oracle-xe-11.2.0-1.0.x86_64.rpm.zip.
Распаковываем его во временном каталоге, переходим в подкаталог "Disk1".
Здесь находится установочный пакет "oracle-xe-11.2.0-1.0.x86_64.rpm". 

2. Проверяем что установлен пакет "bc" и если необходимо, то устанавливаем его командой:
~~~
sudo yum -y install bc
~~~

3. Непосредственно установка Oracle 11g Express Edition
Запускаем установку:
~~~
sudo rpm -ivh oracle-xe-11.2.0-1.0.x86_64.rpm
~~~

После окончания установки необходимо сконфигурировать сервер БД, необходимо задать порты и пароль администратора.
~~~
sudo /etc/init.d/oracle-xe configure
~~~

Проверка успешного запуска
~~~
sudo /etc/init.d/oracle-xe status
~~~

Ручной запуск и остановка соответственно:
~~~
sudo /etc/init.d/oracle-xe start
sudo /etc/init.d/oracle-xe stop
~~~

4. Подготовка к работе
Задем пользователю oracle пароль
~~~
sudo passwd oracle
~~~

Переключаемся на пользователя oracle
~~~
su oracle
~~~

Запускаем командную строку СУБД 
~~~
sqlplus /nolog
~~~
Если есть ошибки при подключении к СУБД, то не забываем про переменные окружения в файле /u01/app/oracle/product/11.2.0/xe/bin/oracle_env.sh


Проверяем работу СУБД, выполняем команду, вводим пароль
~~~
connect system
~~~
После успешного подключения выполняем команду для получения текущей даты
~~~
select current_date as test from dual;
~~~
СУБД работает!!!