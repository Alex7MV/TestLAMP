
Сразу после установки системы не забываем обновить систуму и ее компоненты
~~~
sudo yum -y install update upgrade
~~~


Устанавливаем epel репозиторий ([Extra Packages for Enterprise Linux](https://fedoraproject.org/wiki/EPEL))
~~~
epel-release
~~~

Устанавливаем утилиты для работы с **selinux**
~~~
sudo yum -y install policycoreutils-python
~~~

