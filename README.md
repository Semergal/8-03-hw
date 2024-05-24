# Домашнее задание к занятию «Система мониторинга Zabbix часть 2» - `Трошин Константин`


---

### Задание 1

#### Создайте свой шаблон, в котором будут элементы данных, мониторящие загрузку CPU и RAM хоста.

##### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. В веб-интерфейсе Zabbix Servera в разделе Templates создайте новый шаблон
3. Создайте Item который будет собирать информацию об загрузке CPU в процентах
4. Создайте Item который будет собирать информацию об загрузке RAM в процентах
##### Требования к результаты
1. Прикрепите в файл README.md скриншот страницы шаблона с названием «Задание 1»

### Решение
Назвал task_1 т.к забикс нее дает назвать Задание 1
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_1.jpg)


#### Использовал инструкцию с офф сайта

1. wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-5+debian12_all.deb
2. dpkg -i zabbix-release_6.0-5+debian12_all.deb
3. apt update
4. apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
5. sudo -u postgres createuser --pwprompt zabbix
6. sudo -u postgres createdb -O zabbix zabbix
7. zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
8. systemctl restart zabbix-server zabbix-agent apache2
9. systemctl enable zabbix-server zabbix-agent apache2



### Задание 2
Установите Zabbix Agent на два хоста.

#### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.
#### Требования к результаты
1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
4. Приложите в файл README.md текст использованных команд в GitHub


### Решение
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_2.jpg)
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_3.jpg)
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_4.jpg)

#### Использовал инструкцию с офф сайта
1. wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-5+debian12_all.deb
2. dpkg -i zabbix-release_6.0-5+debian12_all.deb
3. apt update
4. apt install zabbix-agent
5. systemctl restart zabbix-agent
6. systemctl enable zabbix-agent