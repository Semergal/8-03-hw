# Домашнее задание к занятию "`Что такое DevOps. СI/СD`" - `Трошин Константин`


---

### Задание 1

Что нужно сделать:

`Установите себе jenkins по инструкции из лекции или любым другим способом из официальной документации. Использовать Docker в этом задании нежелательно.
Установите на машину с jenkins golang.
Используя свой аккаунт на GitHub, сделайте себе форк репозитория. В этом же репозитории находится дополнительный материал для выполнения ДЗ.
Создайте в jenkins Freestyle Project, подключите получившийся репозиторий к нему и произведите запуск тестов и сборку проекта go test . и docker build ..
В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

1. `Выполнение команд из задания `
![alt text](https://github.com/Semergal/8-03-hw/blob/main/img/Screenshot_1.jpg)

### Задание 2
Что нужно сделать:

Создайте новый проект pipeline.
Перепишите сборку из задания 1 на declarative в виде кода.
В качестве ответа пришлите скриншоты с настройками проекта и результатами выполнения сборки.

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
