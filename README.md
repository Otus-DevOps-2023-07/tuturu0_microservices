# tuturu0_microservices
tuturu0 microservices repository

# ДЗ №20


- Развернуто локальное окружение minikube для работы с Kubernetes
- Развернут Kubernetes в Yandex Cloud
- Запущен reddit в Kubernetes



-----------------------------------------------------------------




# ДЗ №19


- Настроены master и worker-ноды: установлены kubeadm, kubectl, kubelet
- Созданы Deployment манифесты приложений reddit
- Установлен сетевой плагин calico




-----------------------------------------------------------------

# ДЗ №18


- Изучен сбор и фильтрация логов с использованием сервиса post
- Изучен сбор и фильтрация логов с использованием сервиса ui
- Изучены Grok-шаблоны

# Дополнительное задание 1
```bash
<filter service.ui>
  @type parser
  <parse>
    @type grok
    <grok>
      pattern service=%{WORD:service} \| event=%{WORD:event} \| path=%{GREEDYDATA:path} \| request_id=%{GREEDYDATA:request_id} \| remote_addr=%{IPV4:remote_addr} \| method= %{WORD:method} \| response_status=%{INT:response_status}
    </grok>
  </parse>
  key_name message
  # reserve_data true
</filter>
```
Дополнительное задание 2 не делалось


-----------------------------------------------------------------



# ДЗ №17



- Prometheus: запуск, конфигурация, знакомство с Web UI
- Мониторинг состояния микросервисов
- Сбор метрик хоста с использованием экспортера




-----------------------------------------------------------------


# ДЗ №16


- Подготовлена инсталляция Gitlab CI
- Подготовлен репозиторий с кодом приложения
- Создан пайплайн
- Определены окружения


-----------------------------------------------------------------



# ДЗ №15

- Проведены эксперименты с сетевымы драйверами docker
- Создан docker-compose.yml
- Параметризированы некоторые значения при помощи .env
- Создан docker-compose.yml.override

# Имя проекта по умолчанию берётся из каталога docker-compose.yml, можно указать вручную при помощи ключа "-p"
Пример использования:
```Bash
docker compose -p prod up -d
```

-----------------------------------------------------------------


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


-----------------------------------------------------------------

# ДЗ №13


- Базовое знакомство с docker
- Пуш образа docker hub


# ДЗ №12

Заглушка для закрытия ДЗ 12 на сайте otus
