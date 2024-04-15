---
layout: article
---
Теперь займемся поиском образа с приложением. Первый способ - выполнить поиск в пользовательском интерфейсе Docker Hub. Введя в поисковую строку мы получим список всех доступных образов по введенному паттерну. Рядом с названием мы увидим значок, количество загрузок и на какое количество звезд этот образ оценили. Кликнув, мы попадем на страницу описания, а там во вкладке `Tags` мы увидим все версии, которые доступны для скачивания из этого репозитория.

Теги это метки, которые присваиваются образу, чтобы мы могли их отличать. Тегов может быть несколько или тега может не быть. На самом деле, не совсем так. Когда мы создаём контейнер, указав имя образа без тега, предполагается что мы указали тег `latest`. Такой тег latest указывает на последний образ, загруженный в репозиторий.