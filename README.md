=========================================================== HOMEWORK Docker-1 ==============================================================================

-  Установили Докер из репозитория;
-  Запустили контейнеры из шаблонов, скачанных из докер - хаба;
-  Потестировали запуск контейнера, снятие образов;
-  Поработали с командами docker create, docker start, docker run;
-  Посмотрели, как отобразить список образов и список запущенных контейнеров;



ДЗ*

Основные отличия образа от контейнера заключаются в том, что образ - это шаблон в режиме "только чтение". При запуске команды Docker inspect видно, что шабл
он не содержит дополнительных аттрибутов, которые есть у запущенного контейнера.
На основании этого образа - шаблона создается и запускается один или несколько контейнеров. При создании контейнера Docker engine берет образ (файловую систему и метаданые) и запускает контейнер с различными параметрами, такими как сеть, имя контейнера, ресурсы, id, а также с возможностью записи в специальный слой.


# ilya-adm77_microservices
ilya-adm77 microservices repository
