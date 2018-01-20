## [Redis](https://redis.io/)


### Установка
Простая используем версию которая уже есть в yum репозитории
~~~
sudo yum -y install redis
~~~

Запуск
~~~
sudo systemctl start redis.service
sudo systemctl enable redis.service
~~~

Проверка успешного запуска
~~~
sudo systemctl status redis.service
~~~

Запускаем бенчмарк
~~~
redis-benchmark -q -n 1000 -c 10 -P 5
~~~

Проверка работы
~~~
redis-cli
~~~
Выполняем простейшие команды:
~~~
127.0.0.1:6379> set foo bar
OK
127.0.0.1:6379> get foo
"bar"
127.0.0.1:6379> del foo
(integer) 1
127.0.0.1:6379> exists foo
(integer) 0
127.0.0.1:6379>
~~~
