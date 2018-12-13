=========================================================== HOMEWORK Docker-2 ==============================================================================

- Создали новый проект docker в GCP;
- Добавили новый проект в GCP SDK на рабочей машине;
- Установили Docker - machine в облаке;
- Подключились по SSH к докер - хосту в облаке. Запустили несколько контейнеров и проверили
  изоляцию процессов и сети; 
- Если запускать контейнер с флагом docker run --rm --pid host, то в этом случае изоляция PID будет неполная и команда htop
  покажет все процессы хост - машины. Скорее всего подобный режим может использоваться при отладке в случае проблем с контейнером;
- Создали структуру репозитория и заполнили скрипты;
- Создали докер - образ на основе описания в созданном Dockerfile;
- Запустили контейнер реддит, но оказалось, что в ДЗ просят сделать это на удаленном хосте в GCE;
- Передали файлы конфигурации на удаленный хост и пересобрали образ там;
- Запустили контейнер на удаленном докер - хосте и убедились, что приложение доступно на порту 9292,
  открыв перед этим порт 9292 в файрволле GCP;
- Создали учетную запись в Докер хаб и авторизовались в командной строке;
- Сделали пуш образа reddit в докер - хаб;
- Скачали и запустили образ reddit из хаба на локальной машине и убедились что приложение работает
  посредством команды localhost:9292;
- Посмотрели логи контейнера, поработали с процессами, остановили, удалили и пересоздали контейнер; 



=========================================================== HOMEWORK Docker-1 ==============================================================================


-  Настроили интеграцию с чатом
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
