## [nginx ](https://nginx.org/ru/)

### Установка
Устанавливаем nginx как [описано](https://nginx.org/ru/linux_packages.html#stable) на официальнос сайте.

Запускаем его
~~~
service nginx start 
~~~
Проверяем статус
~~~
service nginx start 
~~~

Открываем на файрволе порты для доступа извне и перезапускаем файервол: 
~~~
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
~~~

Файл с настройками находится здесь: /etc/nginx/nginx.conf
