## [nginx ](https://nginx.org/ru/)

### Установка
Устанавливаем nginx как [описано](https://nginx.org/ru/linux_packages.html#stable) на официальнос сайте.

Запуск
~~~
sudo systemctl start nginx.service
sudo systemctl enable nginx.service
~~~

Проверяем статус
~~~
sudo systemctl status nginx.service
~~~

Открываем на файрволе порты для доступа извне и перезапускаем файервол: 
~~~
sudo firewall-cmd --permanent --zone=public --add-service=http
sudo firewall-cmd --permanent --zone=public --add-service=https
sudo firewall-cmd --reload
~~~

Файл с настройками находится здесь: /etc/nginx/nginx.conf
