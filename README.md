# Проект YaMDb (Сборка в Docker контейнер)

## Автор:

💻 [dazdik](https://github.com/dazdik)

![Alt-текст](https://boxboat.com/2017/06/28/whats-new-in-docker-17-06/featured.png "Кит по имени Docker")



## Описание проекта REST API для YaMDb

Создан на основе фреймворка [Django REST Framework (DRF)](https://github.com/ilyachch/django-rest-framework-rusdoc)


Проект YaMDb собирает отзывы пользователей о произведениях. Работы разделены на категории: «Книги», «Фильмы», «Музыка». [Ссылка](https://github.com/dazdik/api_yamdb) на репозиторий с проектом.

____

## Технологии:

- Python 3
- DRF (Django REST framework)
- Django ORM
- Docker
- Gunicorn
- Nginx
- Django 3.2
- PostgreSQL
- GIT
___
## Запуск проекта 🚀

1. Клонировать репозиторий:

```
https://github.com/dazdik/infra_sp2
```

2. Перейти в папку с проектом

```bash
cd infra_sp2
```

3. Перейти в директорию  ```cd infra``` и создать файл .env, заполнить его по следующему примеру:

```
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД
```
4. Запустить docker-compose из папки ```infra```
```bash
docker-compose up -d
```
5. В контейнере web выполнить миграции, создать суперпользователя и собрать статику:
```
docker-compose exec web python manage.py migrate
docker-compose exec web python manage.py createsuperuser
docker-compose exec web python manage.py collectstatic --no-input
```

💥 Теперь проект доступен по адресу http://localhost/admin/

6. Заполнить базу данными:
```
docker-compose exec web python manage.py loaddata fixtures.json
```
___
### Другие команды
*Мониторинг запущенных контейнеров*:
```
docker stats
```

*Оставновить и удалить контейнеры со всеми зависимостями можно командой:*
```
docker-compose down -v
```

*Узнать,  сколько места на диске занимают образы, контейнеры, тома и билд-кеш:*
```
docker system df 
```

*Все неактивные (остановленные) контейнеры удаляются командой:*
```
docker container prune
```

*Удалить образы, какие использовались как промежуточные для сборки других образов, но на которые не ссылается ни один контейнер:*
```
docker image prune
```

*Удалить вообще всё, что не используется (неиспользуемые образы, остановленные контейнеры, тома, которые не использует ни один контейнер, билд-кеш), можно командой:*
```
docker system prune
```