---
layout: article
---
В этом примере  мы сначала создали контейнер с помощью команды `container create`, а затем запустили его при помощи `container start`. Теперь объединим эти две операции в одну.

Для этого мы запускаем команду запуска контейнера docker, которая создает и запускает контейнер из образа.

```
docker container start $(docker container create httpd)
```

Как видишь, это немного громоздко. Есть способ лучше. Запустим контейнер из образа Ubuntu при помощи команды `docker container run`. Это является аналогом предыдущей большой команды.

```
docker  container  run  ubuntu
```

Когда мы запустили эту команду, Docker запустил экземпляр образа Ubuntu и немедленно завершил его работу. Если мы сейчас вызовем `docker container ls`, то не увидим работающих контейнеров. А если мы перечислим вообще все контейнеры, включая остановленные, то увидим, что только что запущенный контейнер находится в состоянии `exit`.

Почему этот docker-контейнер сразу вышел после запуска? Это связано с тем, что, в отличие от виртуальных машин, контейнеры не предназначены для размещения операционной системы как таковой. Контейнеры предназначены для запуска определенной задачи или процесса. Т.е. запуск экземпляра веб-сервера, сервера приложений, базы данных - это подходящая задача. Работа аналитической модели или какое-то задание на какое-то вычисление тоже хороший кейс. Как только задача выполнена, контейнер отключается. Контейнер жив, только если внутри него жив его процесс. Т.е. если веб-служба внутри контейнера сломалась или остановилась, контейнер завершает свою работу.

Ок, вернемся к нашему примеру о том, что когда мы запустили контейнер из образа Ubuntu, и он сразу же вышел. Это связано с тем, что Ubuntu — это образ операционной системы, который предназначен для запуска в себе других процессов. Таким образом, в образе ubuntu по умолчанию не бежит ни один процесс или приложение. И когда мы запускаем контейнер из образа ubuntu, ему нечего делать, поэтому он завершает работу.