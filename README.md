# Разворачиваем PHP + Apache2 + Базы данных в контейнерах

**Предупреждение**  
Проект создан для самостоятельного самообучения, ни в коем случае не воспринимать информацию, как самую надежную. 

## PHP + Apache2
Сборка образа apache2+php
```sh
podman build -t apache_php -f apache_php/Containerfile
```
Запуск контейнера с пробросом портов и директории
```sh
podman run -d -it -p 7000:80 -v $PWD/site/:/var/www/html/ --name apache_php apache_php
```

## MySQL
Сборка образа(по сути переменные добавляем)
```sh
podman build -t mysql -f mysql/Containerfile
```
Запуск контейнера с пробросом портов
```sh
podman run -d -it -p 3306:3306 --name mysql mysql:latest
```

## Поднимаем Pod
Создать pod
```sh
podman pod create --name php_mysql_backend -p 7000:80
```
Добавим в него php + apache + директорию с проектом
```sh
podman run --pod php_mysql_backend -d -it -v $PWD/site/:/var/www/html/ --name apache_php apache_php:latest
```
Добавим mysql/mariadb
```sh
podman run --pod php_mysql_backend -d -it --name mysql mysql:latest
```
