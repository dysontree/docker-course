---
layout: article
---
`nginx` - название образа или репозитория.

Когда мы просто говорим `nginx` в одно слово, на самом деле это `library/nginx`. Первая часть обозначает имя пользователя или учетной записи. Например, если ты сам создал учетную запись на Docker Hub, тогда учетная запись пользователя, которую ты выбрал, является первой частью.

Если мы не укажем здесь имя учетной записи, предполагается, что это библиотечный образ. В данном случае это nginx или library/nginx. Когда ты создашь свою собственную учетную запись и разместишь свои собственные репозитории и образы в них, используй аналогичный шаблон, чтобы до них добраться.

Например, компания nginx создала свои репозитории с названием пользователя `nginx`  и положила туда другие свои популярные образы, например такой, как ингресс-контроллер для Kubernetes. Его мы можем скачать, указав `docker pull nginx/nginx-ingress`.