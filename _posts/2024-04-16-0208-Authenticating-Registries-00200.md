---
layout: article
---
```
docker image pull ubuntu
```

Тут маленькая оговорка насчет Docker Hub. Нам действительно не требуется представляться перед этим реджистри для скачивания образа. Но наш запрос Docker Hub запоминает. И если мы будем слишком часто пуллить анонимно, он может нам в этом отказать. Обратно, если мы представимся в этом реджистри, то наши квоты будут увеличены.

Ок, если мы попробуем спуллить образ из приватного реестра, мы получим ошибку доступа.

```
docker image pull cr.yandex/crp41679661gmc8dsf1d/private-os/ubuntu
```

Также, если ты собрался отправить свой кастомный образ на хранение в публичный или приватный репозиторий, то тебе также придется аутентифицироваться.

```
docker image push ubuntu
```

Давай на это посмотрим. Т.е. на то, как именно нам зайти в docker-реджистри.