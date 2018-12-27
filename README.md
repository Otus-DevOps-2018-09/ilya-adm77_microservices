=========================================================== HOMEWORK Gitlab-ci-1  ===========================

Основное ДЗ:

- С помощью docker-machine создали в облаке докер - хост с нужными аппаратными ресурсами;
- Установили docker-compose и создали yml - описание процесса установки Gitlab с помощью образа omnibus;
- Получили доступ к веб - интерфейсу Gitlab после установки;
- Отключили регистрацию новых пользователей и начали описывать проект;
- Создали группу и проект; Подключили репозиторий гитлаб;
- Создали и добавили в репозиторий (локальный и гитлаб) файл .gitlab-ci.yml;
- Содали и запустили новый раннер на докер - хосте;
- После добавления раннера пайплайн запустился и тесты прошли успешно;
- Добавили исходный код reddit в репозиторий;
- Добавили тесты для приложения, отправили изменения в гитлаб;
- Теперь после каждого изменения прогоняются тесты;

ДЗ со *

- Настроена интеграция с Slack - чатом. Приходят уведомления о пуше в репо и пайплайнах (активировал
  только эти опции) Ссылка на канал: #ilya_nikolskiy
  https://devops-team-otus.slack.com/messages/CDC3TFHMM/details/
- Настроим автоскейлинг раннера, опираясь на официальную документацию Gitlab, шаги по настройке указаны   в файле install.txt, настройки раннера в файле config.toml. Всё лежит в папке gitlab в
  репозитории.


=========================================================== HOMEWORK Docker-4 ====================================

Основное ДЗ

- Подключились к докер-хосту в GCP;
- Запустили контейнер из образа joffotron/docker-net-tools cначала без
  поддержки сети. Убедились, что доступен только loopback - интерфейс;
- Запустили тот же контейнер с параметром --network;
- Запустили 4 раза контейнер nginx командой docker run --network host -d nginx,
  но при запуске команды docker ps увидели, что остался запущенным только первый
  контейнер. В логах остальных контейнеров видно, что из-за общего доступа к сети
  (флаг --network host) остальные контейнеры не смогли корректно работать с IP - адресами
  и поэтому их работа в бэкграунде (флаг -d) завершалась. Если запускать контейнеры без
  флага --network, то все контейнеры будут работать.
- Пересоздали контейнеры с параметрами --network host и --network none и посмотрели командой ip netns,
  как меняется список namespace-ов; 
- Создали bridge-сеть reddit на докер-хосте;
- Запустили проект reddit с использованием bridge - сети;
- Без задания алиасов приложение не работает нормально;
- Пересоздали контейнеры с алиасами, приложение корректно запустилось;
- Попытка перезапустить проект в двух bridge - сетях; Удалили все контейнеры;
- Cоздали две подсети 10.0.2.0/24 и 10.0.1.0/24 с тегами back_net и front_net;
- Пересоздали контейнеры с этими тэгами; Но приложение корректно не открывается;
- Поместили контейнеры post и comment в обе сети;
- Установили bridge-utils и с помощью brctl show посмотрели veth-интерфейсы;
- В iptables посмотери правила проброса порта 9292 и правила, которые выпускают контейнеры во внешнюю сеть;
Docker Compose
- Установили утилиту docker-compose;
- создали файл docker-compose.yml в репозитории;
- Остановили контейнеры, сделали экспорт переменной USERNAME и запустили приложение
  с помощью docker-compose. Проверили, приложение работает, docker-compose ps показывает список
  контейнеров;
Задание:
- Измениили docker - compose для работы с нескольскими сетями, в файле docker-compose.yml
  показан пример создания сетей back_net и front_net;
- Создали файл .env в директории src, в котором задали переменные для порта сервиса, версии ui
  и подсети для front_net. Переменные отражены в docker-compose.yml;
- docker-compose читает переменные из файла .env при запуске инфраструктуры;
- Имя проекта можно задать также в файле .env посредством переменной COMPOSE_PROJECT_NAME=FOO,
  тогда все сущности будут создаваться с нужным префиксом;

Задание со *

- Попробовал самый простой метод. Залил исходные файлы проекта из папки src на докер-хост в облаке;
- Смонтировал папку с проектом в папку приложения в контейнере для всех 3-х приложений; 
- Теперь можно менять исходный код и смотреть изменения без ребилда всего образа целиком;
- puma запускается в дебаг - режиме, все изменения прописаны в файле docer-compose.override;

=========================================================== HOMEWORK Docker-3 ====================================
Основное ДЗ*
- Подключились к докер - хосту в облаке;
- Скачали в репозиторий архив с микросервисами;
- Создали докер - файл для каждого микросервиса;
- На основе этих докер - файлов создали образы контейнеров на удаленном хосте;
- Скачали свежий образ БД Монго;
- Создали сеть для приложения и запустили 4 контейнера на удаленном хосте;
- Проверили запуск и работу приложения, пройдя по ссылке 'ip-адрес удаленной машины:9292';

Задание с *

- Остановили все контейнеры;
- Чтобы запустить контейнеры с новыми алиасами без пересоздания образов, попробуем переопределить
  переменные окружения, изначально заданные в докер - файле:
  $docker run -d --network=reddit --network-alias=post_db11 --network-alias=comment_db11 mongo:latest
  $docker run -d --network=reddit -e POST_DATABASE_HOST='post_db11' --network-alias=post11 otusdevops77/post:1.0
  $docker run -d --network=reddit -e COMMENT_DATABASE_HOST='comment-db11' --network-alias=comment11 otusdevops77/   comment:1.0
  $docker run -d --network=reddit -p 9292:9292 -e COMMENT_SERVICE_HOST='comment11' -e POST_SERVICE_HOST='post11' o  tusdevops77/ui:1.0
- Проверили, что приложение запускается, посты добавляются. Значит переопределение алиасов работает;

Основное ДЗ

- Образы с микросервисами занимают много места, измени докер - файл для образа ui;
- Пересобрали образ ui версии 2.0 и убедились, что теперь он занимает 453Мб, а не 781Мб;

Задание со *

- Создали образ ui с помощью Alpine Linux. Инструкции по созданию добавили в Dockerfile.1;
- После создания файл образа уменьшился до 216Мб;
- Попробуем уменьшить размер образа:
  1. Создадим докер файл Dockerfile.2;
  2. Уменьшим количество слоев, объединив директивы RUN для установки пакетов;
  3. Почистим кэш apk;
  В результате полученный образ весит уже 214Мб, а не 216. Помогло, но не сильно.
- Прогнали Dockerfile.2 через линтер fromlatest.io. Линтер посоветовал использовать
  команду RUN apk --no-cache при добавлени пакетов. Пересоздали образ, но размер остался
  тем же.
- Удалили все лишние пакеты из докер-файла. Создали Dockerfile.3. После сборки размер образа
  получился 211Мб.

Основное ДЗ

- Пересоздали все контейнеры и оказалось, что изменения в бд не были сохранены;
- Создали docker volume reddit_db и подключили к контейнеру mongoDB;
- Пересоздали контейнеры, написали пост;
- Удалили и пересоздали контейнеры. Убедились, что пост на месте.




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
- Запустили контейнер reddit на удаленном докер - хосте и убедились, что приложение доступно на порту 9292,
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
