---
layout: article
---
То, что сейчас мы называем Docker Swarm - это встроенный в Docker набор технологий и инструментов, который идёт в базовой поставке. И более точно это называется `Docker Swarm Mode`. Но раньше было не так. Подобно старому `docker-compose` был отдельный бинарник оркестратора контейнеров. Сейчас этот продукт называется `Docker Swarm Classic` и он перестал обновляться в 2018 году. Поэтому далее мы говорим только о встроенном режиме Docker Swarm.

Идея режима Docker Swarm состоит в том, чтобы предоставить единый интерфейс в Docker CLI, чтобы но этот интерфейс работал с позиций не отдельного docker-демона, а управлял с перспективы набора таких демонов, т.е. кластера. Проект бурно развивался на своём старте, сейчас развитие замедлилось, но он имеет все атрибуты для организации продуктовых кластеров: в нём есть несколько плагинов-планировщиков, которые реализуют разные стратегии назначения контейнеров на хосты, а также встроенный service discovery.

Поле оркестрации контейнеров (если отбросить специфичные оркестраторы, которые используются в крупных облаках) делят две технологии: Kubernetes и Docker Swarm. Остальные standalone проекты или занимают очень специфичную нишу, или мертвы.
Когда мы видим популярные оркестраторы, например, OpenShift или Rancher, надо понимать, что это адаптация Kubernetes. Kubernetes очень открытая и гибкая система, у нее гигантское комьюнити. Kubernetes может обслуживать как колоссальные нагрузки, так и совсем маленькие. Но также эта система более сложная в части того, как она сделана изнутри, и в части того, как её настроить под свои нагрузки.