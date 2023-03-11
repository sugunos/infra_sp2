# YaMDb API

### Описание проекта:

Проект YaMDb собирает отзывы пользователей на произведения, позволяет ставить произведениям оценку и комментировать чужие отзывы.

Произведения делятся на категории, и на жанры. Список произведений, категорий и жанров может быть расширен администратором.

Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

Доступ к БД проекта осуществляется через Api.
### Технологии
Python 3.7
Django 2.2.19
Gunicorn 20.0.4
Nginx 1.21.3

Полный список запросов и эндпоинтов описан в документации ReDoc, доступна после запуска проекта по адресу:
```
http://127.0.0.1:8000/redoc/
```

### Как запустить проект в контейнерах:
Клонировать репозиторий, перейти в директорию с проектом.

```
git clone git@github.com:sugunos/api_yamdb.git
```

Запустить docker-compose

```
sudo docker-compose up
```
Выполнить миграции
```
docker-compose exec web python manage.py migrate
```

Собрать статику

```
docker-compose exec web python manage.py collectstatic --no-input 
```

### Шаблон наполнения .env-файла

```
DB_ENGINE=указываем, что работаем с postgresql
DB_NAME=имя базы данных
POSTGRES_USER=логин для подключения к базе данных
POSTGRES_PASSWORD=пароль для подключения к БД
DB_HOST=название сервиса (контейнера)
DB_PORT=порт для подключения к БД
SECRET_KEY=секретный ключ

```



### Авторизация пользователей:
Для получения доступа необходимо создать пользователя отправив POST запрос на эндпоинт ```/api/v1/auth/signup/``` username и email

Запрос:
```
{
"email": "string",
"username": "string"
}
```
После этого на email придет код подтверждения, который вместе с username необходимо отправить POST запросом на эндпоинт```/api/v1/auth/token/```

Запрос:
```
{
"username": "string",
"confirmation_code": "string"
}
```
Ответ:
```
{
"access": "string"
}
```
Полученный токен используется для авторизации

Для просмотра и изменения своих данных используйте эндпоинт ```/api/v1/users/me/```

### Примеры запросов к API:

Получение списка всех категорий:

```
http://127.0.0.1:8000/api/v1/categories/
```
Получение списка всех жанров:

```
http://127.0.0.1:8000/api/v1/genres/
```

Получение списка всех произведений:

```
http://127.0.0.1:8000/api/v1/titles/
```

