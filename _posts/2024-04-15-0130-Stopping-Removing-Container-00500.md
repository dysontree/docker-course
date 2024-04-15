---
layout: article
---
Помимо этих команд, мы также можем отправлять нужные нам сигналы процессу внутри контейнера при помощью команды `docker container kill`. Здесь, как и в случае с командой kill сверху, мы можем передать конкретный сигнал в качестве опции `--signal`.

```
docker container kill --signal=9  web
```

```
docker  container  ls 
```

Давай теперь посмотрим на удаление остановленного контейнера. Для этого действия есть команда `docker container rm`. Она навсегда удалит не работающий в этот момент контейнер. Т.е он должен быть остановленным или вышедшим. 

```
docker container rm web
```

Если попробовать проделать это на работающем контейнере, мы получим ошибку, в которой говорится, что мы не можем удалить бегущий контейнер. Таким образом, полное удаление контейнера представляет собой двухэтапный процесс. Сначала нам нужно его остановить с помощью команды `docker container stop` и только после этого удалить его.

```
docker container stop web && docker container rm web
```

Как мы обсуждали ранее, при создании контейнера формируется структура каталогов для компонентов Docker. По умолчанию это происходит в каталоге `/var/lib/docker/containers`. Мы можем увидеть список контейнеров хоста, заглянув в него. 

```
ls -al /var/lib/docker/containers/
```

Когда мы приостанавливаем или останавливаем контейнер, структура каталогов остаётся неизменной. Именно это позволяет нам запустить его снова или возобновить работу контейнера в будущем. Но когда мы удалим контейнер, это полностью удалит эту структуру каталогов и очистит место на нашем диске. Здесь я удалил работающий контейнер одной командой, используя опцию `-f`. Это быстрый способ удаления контейнера, аналог сигнала `SIGKILL`. 

```
docker container rm -f web
```

```
ls -al /var/lib/docker/containers/
```

Имей в виду, что такая команда не подходит, если у тебя несколько контейнеров и они общаются друг с другом.
Теперь перед нами стоит задача удалить все контейнеры с нашего хоста. Запустим `docker container ls`.