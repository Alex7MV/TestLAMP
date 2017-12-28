## [nginx ](https://nginx.org/ru/) 


Открываем на файрволе порты для доступа извне и перезапускаем файервол: 
~~~
firewall-cmd --permanent --zone=public --add-service=http
firewall-cmd --permanent --zone=public --add-service=https
firewall-cmd --reload
~~~

