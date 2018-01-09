## [Docker](https://www.docker.com/)

### Установка
Устанавливаем Docker 
~~~
$ curl -fsSL https://get.docker.com/ | sh
~~~

После установки вам предложат добавить пользователя в группу docker командой: 
~~~
$ sudo usermod -aG docker you_user
~~~

Запускаем
~~~
$ sudo systemctl start docker
~~~

Проверяем статус
~~~
$ sudo systemctl status docker
~~~

