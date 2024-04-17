---
layout: article
---

Второй вариант - рост в горизонтальной плоскости. Мы берём несколько серверов и учим их работать вместе, деля обязанности и помогая друг другу. Это обычно дешевле, эффективнее и удобнее для обслуживания. Но также это требует специальной системы для работы этих хостов в режиме кластера. Такое программное обеспечение называется оркестратором. Что-то вроде дирижёра, который будет приглядывать за узлами кластера и за рабочими нагрузками на них.

С точки зрения Docker, это как если бы мы запустили экземпляры Docker Compose на нескольких узлах и научили их координировать свою деятельность. Им бы понадобилась собственная безопасная среда для общения, им потребовался бы механизм проверки, все ли узлы здоровы и всем ли хватает ресурсов, им нужен механизм распределения контейнеров по узлам, еще необходимо, чтобы трафик, попавший в кластер находил свои контейнеры, которые теперь разбросаны по узлам и еще 1001 задача. Вот так появился `Docker Swarm`.