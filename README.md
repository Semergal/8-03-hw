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



### Задание 2
Добавьте в Zabbix два хоста и задайте им имена <фамилия и инициалы-1> и <фамилия и инициалы-2>. Например: ivanovii-1 и ivanovii-2.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 виртмашины, одной из них может быть ваш Zabbix Server
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera
5. Прикрепите за каждым хостом шаблон Linux by Zabbix Agent
6. Проверьте что в разделе Latest Data начали появляться данные с добавленных агентов
#### Требования к результаты
Результат данного задания сдавайте вместе с заданием 3


### Задание 3
Привяжите созданный шаблон к двум хостам. Также привяжите к обоим хостам шаблон Linux by Zabbix Agent.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Зайдите в настройки каждого хоста и в разделе Templates прикрепите к этому хосту ваш шаблон
3. Так же к каждому хосту привяжите шаблон Linux by Zabbix Agent
4. Проверьте что в раздел Latest Data начали поступать необходимые данные из вашего шаблона
#### Требования к результаты
Результат данного задания сдавайте вместе с заданием 3

### Решение
По 2 пункту есть проблема в новой версии забикса нельзя прикрутить шаблон с item который уже есть в другом шаблоне, а именно из пункта 3 Linux by Zabbix Agent
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_2.jpg)

![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_3.jpg)

Данные поступают
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_4.jpg)


### Задание 4
Создайте свой кастомный дашборд.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. В разделе Dashboards создайте новый дашборд
3. Разместите на нём несколько графиков на ваше усмотрение.

### Решение
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_5.jpg)