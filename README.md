# Домашнее задание к занятию 12 «GitLab»

## Подготовка к выполнению


1. Или подготовьте к работе Managed GitLab от yandex cloud [по инструкции](https://cloud.yandex.ru/docs/managed-gitlab/operations/instance/instance-create) .
Или создайте виртуальную машину из публичного образа [по инструкции](https://cloud.yandex.ru/marketplace/products/yc/gitlab ) .
2. Создайте виртуальную машину и установите на нее gitlab runner, подключите к вашему серверу gitlab  [по инструкции](https://docs.gitlab.com/runner/install/linux-repository.html) .

<img width="1113" alt="Gitlab VM" src="https://github.com/user-attachments/assets/954449cb-f1fc-4661-9808-99396111742b">


3. (* Необязательное задание повышенной сложности. )  Если вы уже знакомы с k8s попробуйте выполнить задание, запустив gitlab server и gitlab runner в k8s  [по инструкции](https://cloud.yandex.ru/docs/tutorials/infrastructure-management/gitlab-containers). 

4. Создайте свой новый проект.

<img width="774" alt="Project" src="https://github.com/user-attachments/assets/3be4bfd9-3c33-449e-8efc-3c9b48662d0a">
   
5. Создайте новый репозиторий в GitLab, наполните его [файлами](./repository).

<img width="806" alt="Add file in repo" src="https://github.com/user-attachments/assets/c9ad622a-b20c-44c6-b073-f8e147727756">

6. Проект должен быть публичным, остальные настройки по желанию.

## Основная часть

### DevOps

В репозитории содержится код проекта на Python. Проект — RESTful API сервис. Ваша задача — автоматизировать сборку образа с выполнением python-скрипта:

1. Образ собирается на основе [centos:7](https://hub.docker.com/_/centos?tab=tags&page=1&ordering=last_updated).
2. Python версии не ниже 3.7.
3. Установлены зависимости: `flask` `flask-jsonpify` `flask-restful`.
4. Создана директория `/python_api`.
5. Скрипт из репозитория размещён в /python_api.
6. Точка вызова: запуск скрипта.
7. При комите в любую ветку должен собираться docker image с форматом имени hello:gitlab-$CI_COMMIT_SHORT_SHA . Образ должен быть выложен в Gitlab registry или yandex registry.   

<img width="460" alt="Registered runners" src="https://github.com/user-attachments/assets/5c00a33f-cbed-4d05-a8e7-8711aecd5d53">

<img width="774" alt="Project" src="https://github.com/user-attachments/assets/8b8b78e3-06f0-4a7b-8e2f-6cae31b7ddab">

<img width="1030" alt="Container Registry" src="https://github.com/user-attachments/assets/0d3a153f-5c81-4186-970c-8b56f05f9948">

<img width="1004" alt="Gitlab-ci" src="https://github.com/user-attachments/assets/1a5f1adb-ac2c-4823-aa21-133de7e85ef4">

[Репозиторий](https://gitlab.com/sash3939/gitlab)

[Registry](https://gitlab.com/sash3939/gitlab/container_registry)

[gitlab-ci](https://gitlab.com/sash3939/gitlab/-/blob/main/.gitlab-ci.yml?ref_type=heads)

### Product Owner

Вашему проекту нужна бизнесовая доработка: нужно поменять JSON ответа на вызов метода GET `/rest/api/get_info`, необходимо создать Issue в котором указать:

1. Какой метод необходимо исправить.
2. Текст с `{ "message": "Already started" }` на `{ "message": "Running"}`.
3. Issue поставить label: feature.

### Developer

Пришёл новый Issue на доработку, вам нужно:

1. Создать отдельную ветку, связанную с этим Issue.
2. Внести изменения по тексту из задания.
3. Подготовить Merge Request, влить необходимые изменения в `master`, проверить, что сборка прошла успешно.


### Tester

Разработчики выполнили новый Issue, необходимо проверить валидность изменений:

1. Поднять докер-контейнер с образом `python-api:latest` и проверить возврат метода на корректность.
2. Закрыть Issue с комментарием об успешности прохождения, указав желаемый результат и фактически достигнутый.

## Итог

В качестве ответа пришлите подробные скриншоты по каждому пункту задания:

- файл gitlab-ci.yml;
- Dockerfile; 
- лог успешного выполнения пайплайна;
- решённый Issue.

### Важно 
После выполнения задания выключите и удалите все задействованные ресурсы в Yandex Cloud.
