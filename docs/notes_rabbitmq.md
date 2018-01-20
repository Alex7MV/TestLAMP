## [RabbitMQ](https://www.rabbitmq.com/)
[Ссылка](https://www.rabbitmq.com/install-rpm.html) на официальное руководство по установке.

### Установка
В yum репозитории находится не самоя последняя версия RabbitMQ, лучше загрузить и установить последнюю версиб с сайта. 

Устанавливаем Erlang на котором написан RabbitMQ, см. инструкцию злесь: https://github.com/rabbitmq/erlang-rpm 

Устанавливаем RabbitMQ из RPM:
~~~
sudo rpm --import https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc
sudo rpm -Uvh https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.2/rabbitmq-server-3.7.2-1.el7.noarch.rpm
~~~

Запуск
~~~
sudo systemctl start rabbitmq-server.service
sudo systemctl enable rabbitmq-server.service
~~~

Проверка успешного запуска
~~~
sudo systemctl status rabbitmq-server.service
~~~

### Доступ
Используемые порты:
~~~
4369: epmd, a peer discovery service used by RabbitMQ nodes and CLI tools
5672, 5671: used by AMQP 0-9-1 and 1.0 clients without and with TLS
25672: used by Erlang distribution for inter-node and CLI tools communication and is allocated from a dynamic range (limited to a single port by default, computed as AMQP port + 20000). See networking guide for details.
15672: HTTP API clients and rabbitmqadmin (only if the management plugin is enabled)
61613, 61614: STOMP clients without and with TLS (only if the STOMP plugin is enabled)
1883, 8883: (MQTT clients without and with TLS, if the MQTT plugin is enabled
15674: STOMP-over-WebSockets clients (only if the Web STOMP plugin is enabled)
15675: MQTT-over-WebSockets clients (only if the Web MQTT plugin is enabled)
~~~
Для работы из PHP по протоколу AMQP нам необходимо открыть порт 5672.
Настраиваем фаервол:
~~~
sudo firewall-cmd --permanent --add-port=5672/tcp
sudo firewall-cmd --reload
~~~

По умолчанию создается пользователь guest с паролем guest, но с ограниченными правами доступа только к localhost.
Сделано это в целях безопастности, чтобы этот пользователь не использлвался в рабочих системах и они не быди поверженны несанкционированному доступу или взлому злоумышлинниками.
