
Сразу после установки системы не забываем обновить систуму и ее компоненты
~~~
$ sudo yum -y install update upgrade
~~~


Устанавливаем epel репозиторий ([Extra Packages for Enterprise Linux](https://fedoraproject.org/wiki/EPEL))
~~~
$ sudo yum -y install epel-release
~~~

Устанавливаем утилиты для работы с **selinux**
~~~
$ sudo yum -y install policycoreutils-python
~~~


### SAMBA
Установка
~~~
$ sudo yum -y install samba samba-client samba-common
~~~

Добавление службы в автоматический запуск
~~~
$ sudo chkconfig smb on
~~~

Запуск службы и проверка состояния
~~~
$ sudo service smb start
smbstatus 
~~~

FrewallD создаем правило для SAMBA и перезагружаем
~~~
$ sudo firewall-cmd --permanent --zone=public --add-service=samba
$ sudo firewall-cmd --reload 
~~~

#### Анонимный доступ средствами samba


https://bozza.ru/art-262.html