# tuturu0_microservices
tuturu0 microservices repository

# ДЗ №14


- Собраны образы для сервисов post-py, comment, ui
- Созданы контейнеры
- Сборка ui началась не с первого шага, т.к. начальные шаги сборки были в кэше после сборки comment, которая была ранее
- Создана сеть bridge reddit, чтобы обойти ограничение обращений только по адресам
- В образы на основе ruby пришлось добавить архивный репозиторий
- Для образа post-py необходимо добавить в requirements.txt "markupsafe==1.1.1" или использовать в качестве базового образа FROM python:3.6-alpine
- Образ mongo:latest не работает, так что использовался mongo:4
- Для сохранения постов для контейнера с mongo создан volume

# Дополнительное задание
Изменение алиасов и переменных окружения без переписывания Dockerfile представлено ниже:
```Bash
docker run -d --network=reddit \
  --network-alias=post_db_new --network-alias=comment_db_new \
  mongo:4

docker run -d --network=reddit \
  --network-alias=post_new \
  --env POST_DATABASE_HOST=post_db_new \
  tuturu0/post:1.0

docker run -d --network=reddit \
  --network-alias=comment_new \
  --env POST_DATABASE_HOST=comment_db_new \
  tuturu0/comment:1.0

docker run -d --network=reddit -p 9292:9292 \
  --env POST_SERVICE_HOST=post_new \
  --env COMMENT_SERVICE_HOST=comment_new \
  tuturu0/ui:1.0
```

# Для оптимизации использовался образ на основе ubuntu (файл Dockerfile_ubuntu)
# Второе дополнительное задание:
Образ пересобран на основе alpine:3.14 (файл Dockerfile_alpine)


#-----------------------------------------------------------------

# ДЗ №13


- Базовое знакомство с docker
- Пуш образа docker hub


#ДЗ №12

Заглушка для закрытия ДЗ 12 на сайте otus
