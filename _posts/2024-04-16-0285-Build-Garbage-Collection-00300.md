---
layout: article
---

В демоне BuildKit реализован механизм сборки мусора. Демон очищает кэш сборки, когда его размер становится слишком большим или когда истекает срок хранения кэша. По умолчанию в нём уже выставлены несколько policies:

- если кэш сборки использует более 512 МБ, удаляем данные, если они не использовались в течение 2 дней.
- удалять любые данные, которые не использовались в течение 60 дней.
- держать общий размер кэша сборки не более 10% от объёма диска.
- если предыдущих политик недостаточно, и кэш не уменьшился, то принудительно удалять данные, чтобы стало не более 10% диска.

Мы можем настроить эти политики жизненного цикла кэширования под себя.

Конфигурация будет немного разной для разных драйверов сборки, вот пример для драйвера `docker`:

```
{
  "builder": {
    "gc": {
      "enabled": true,
      "policy": [
        { "keepStorage": "10GB", "filter": ["unused-for=2200h"] },
        { "keepStorage": "50GB", "filter": ["unused-for=3300h"] },
        { "keepStorage": "100GB", "all": true }
      ]
    }
  }
}
```

Эти настройки можно положить в файл конфигурации демона, который по умолчанию находится в `/etc/docker/daemon.json`. Обрати внимание, что для других драйверов сборщика порядок будет другим. Также имей в виду, что в базовой настройке garbage collector отключен.

Мы можем посмотреть, эффективны ли настройки командой `docker builder inspect`.

```
DOCKER_BUILDKIT=1 docker builder inspect
```

Какие проблемы могут быть при использовании BuildKit GC?

- проверка ведётся только по накопленному объёму файлов и возрасту элементов кэша. Но в некоторых СХД у него не получается верно определить объем, и мы можем получить ошибку `ENOSPC`.
- то же самое и с inodes, BuildKit их просто не учитывает. Для определения наличия индексных дескрипторов придется использовать дополнительный скрипт.

Далее я приведу несколько моментов, которые я использую, чтобы улучшить свои конвейеры CI.

- BuildKit управляет локальным кэшем, хранящимся на `локальной` файловой системе. Таким образом, нам нужно использовать быстрый постоянный диск. Т.е. данные должны сохраняться независимо от статуса `buildkitd`. Таким образом, запуская это в кластере Kubernetes, нужно иметь примонтированный постоянный том. Я обычно выбираю что-то из нереплицируемых облачных SSD-дисков, которые очень быстрые и недорогие.
- каждому одновременно выполняющемуся процессу `buildkitd` должен быть выделен свой дисковый том. BuildKit не поддерживает одновременные операций чтения и записи в свой локальный кэш.
- политики GC по умолчанию не подходят для CI-сред. В `KeepBytes` установлено очень маленькое значение - 10% от емкости диска. То же самое для элементов кэша типа `exec.cachemount`. Каждая папка кэша, размер которой превышает 512 МБ и старше 2 дней, будет удалена. На практике предел в 512 МБ почти сразу же превышается, а 2-х дневное хранение замедляет системы по понедельникам, поскольку два дня выходных приговаривают любые кэши к удалению.
- используй `inline` и `registry` кэши с тем же репозиторием, для которого собираешь образ. Это ускоряет нас в том, что часть слоёв уже находится в реджистри, и системе не придётся перезаливать их на серверы при пуше. Но тут есть много подводных камней в зависимости от твоего `gitflow`, т.к. процесс работы с удаленным кэшем может работать неверно при масштабировании экземпляров `buildkitd`.

Ок, всё это звучит как общие рекомендации, а я больше люблю конкретику. Но всё же здесь не буду погружаться в детали, поскольку сборка в CI разных типов приложений создаёт разный характер проблем: от огромных объёмов данных кэшей для `Gradle` до нехватки inodes для `Yarn`. 

Основной посыл лекции в том, что кэши в Docker в процессе сборок всё равно заглючат, что в Docker есть команды для очистки кэша, а также есть механизмы для автоматизации этого процесса.

Это всё, увидимся!
