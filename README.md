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
