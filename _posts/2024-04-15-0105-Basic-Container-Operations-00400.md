---
layout: article
---
Ок, команда `docker container list` или короче `ls` выводит список всех запущенных контейнеров и показывает базовую информацию о каждом из них, такую как идентификатор контейнера, имя образа, который мы использовали для его запуска, текущий статус и имя контейнера. Чтобы просмотреть все запущенные контейнеры, независимо от того, работают они или нет, используй параметр `-a`. Это выводит созданные, работающие и остановленные контейнеры. В нашем случае это контейнер, который мы создали ранее из образа `httpd`. 

Ниже приведены несколько полезных опций. Если мы используем опцию `-l` с командой `ls`, то увидим сведения о последнем созданном контейнере. Параметр `-q` отобразит короткий идентификатор контейнера. Без параметра `-a` это выведет IDs только для запущенных контейнеров, и в нашем случае вывод пуст, поскольку наш контейнер был только создан, но еще не запущен. Опция `-qa` отобразит короткие идентификаторы для всех имеющихся контейнеров.