# Домашнее задание к занятию «Система мониторинга Zabbix» - `Трошин Константин`


---

### Задание 1

Установите Zabbix Server с веб-интерфейсом.

Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
Требования к результаты
Прикрепите в файл README.md скриншот авторизации в админке.
Приложите в файл README.md текст использованных команд в GitHub.

1. `Выполнение команд из задания `
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_1.jpg)


Использовал инструкцию с офф сайта

Установите и сконфигурируйте Zabbix для выбранной платформы
a. Установите репозиторий Zabbix
Документация
wget https://repo.zabbix.com/zabbix/6.0/debian/pool/main/z/zabbix-release/zabbix-release_6.0-5+debian12_all.deb
dpkg -i zabbix-release_6.0-5+debian12_all.deb
apt update
b. Установите Zabbix сервер, веб-интерфейс и агент
apt install zabbix-server-pgsql zabbix-frontend-php php8.2-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent
c. Создайте базу данных
Документация
Установите и запустите сервер базы данных.

Выполните следующие комманды на хосте, где будет распологаться база данных.

sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль.

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
d. Настройте базу данных для Zabbix сервера
Отредактируйте файл /etc/zabbix/zabbix_server.conf

DBPassword=password
e. Запустите процессы Zabbix сервера и агента
Запустите процессы Zabbix сервера и агента и настройте их запуск при загрузке ОС.

systemctl restart zabbix-server zabbix-agent apache2
systemctl enable zabbix-server zabbix-agent apache2
f. Open Zabbix UI web page
The default URL for Zabbix UI when using Apache web server is http://host/zabbix


### Задание 2
Установите Zabbix Agent на два хоста.

Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.
Требования к результаты
Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
Приложите в файл README.md текст использованных команд в GitHub

![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_2.jpg)
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_3.jpg)
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_4.jpg)
```
pipeline {
 agent any
 stages {
  stage('Git') {
   steps {git 'https://github.com/Semergal/sdvps-materials8.git'}
  }
  stage('Test') {
   steps {
    sh '/usr/local/go/bin/go test .'
   }
  }
  stage('Build') {
   steps {
    sh 'docker build -f Dockerfile .'
   }
  }
 }
}
```

---

### Задание 3

Что нужно сделать:

Установите на машину Nexus.
Создайте raw-hosted репозиторий.
Измените pipeline так, чтобы вместо Docker-образа собирался бинарный go-файл. Команду можно скопировать из Dockerfile.
Загрузите файл в репозиторий с помощью jenkins.
В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_5.jpg)
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_6.jpg)

```
pipeline {
    agent any
    environment {
        PATH = "/usr/local/go/bin:${env.PATH}"
    }
    stages {
        stage('Checkout') {
            steps {
                script {
                    git 'https://github.com/netology-code/sdvps-materials.git'
                }
            }
        }
        stage('Build Go Binary') {
            steps {
                script {
                    sh 'CGO_ENABLED=0 GOOS=linux go build -a -installsuffix nocgo -o app .'
                }
            }
        }
        stage('Upload to Nexus') {
            steps {
                script {
                    sh 'curl -v --user admin:admin --upload-file app http://192.168.1.56:8081/repository/8-02/'
                }
            }
        }
    }
}
```
