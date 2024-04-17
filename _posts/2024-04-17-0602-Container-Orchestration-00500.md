---
layout: article
---

Плюсы Docker Swarm - её простота в установке и простота в деплое приложений. Если мы установили Docker, мы автоматически имеем и Swarm. Мы сразу получаем распределенное хранилище для кластера, которое зашифровано, имеем зашифрованные сети, взаимный TLS, безопасное присоединение к кластеру по токену, систему PKI, которая позволяет управлять и ротировать сертификаты. Мы можем динамически добавлять и удалять узлы без остановки кластера. Мы можем бесшовно обновлять свои приложения, чтобы пользователи не видели простоя. Эти развертывания мы можем декларативно описать в compose-файлах. Также есть и ручной режим, в котором мы можем императивно управлять нагрузками.

Минусы Docker Swarm те же самые - простота и малая гибкость.

Кластеры Swarm могут содержать одного или нескольких менеджеров, которые действуют как центры управления кластером docker-хостов. Лучше всего, чтобы менеджеров было нечетное число. Одновременно только один менеджер будет выступать в роли лидера кластера. Также можно добавлять рабочие узлы, которые не участвуют в управлении. Нагрузки можно размещать и на менеджерах, но в больших кластерах так не стоит делать.

Давай посмотрим на особенности Swarm в следующей лекции. Жду тебя там.