# YaMDb API

### Описание проекта:

Проект YaMDb собирает отзывы пользователей на произведения, позволяет ставить произведениям оценку и комментировать чужие отзывы.

Произведения делятся на категории, и на жанры. Список произведений, категорий и жанров может быть расширен администратором.

Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.

Доступ к БД проекта осуществляется через Api.
### Технологии
- Python 3.7
- Django 3.2
- Django REST Framework 3.12.4
- Gunicorn 20.0.4
- Nginx 1.21.3

### Полный список запросов и эндпоинтов описан в документации ReDoc, доступна после запуска проекта по адресу:
```
localhost/redoc/
```

### Как запустить проект в контейнерах:
Клонировать репозиторий, перейти в директорию с проектом.

```
git clone git@github.com:sugunos/infra_sp2.git
```
Перейти в директорию с docker-compose.yaml
```
cd infra_sp2/infra/
```
Создать и заполнить .env-файл по шаблону:
```
DB_ENGINE=указываем, что работаем с postgresql
DB_NAME=имя базы данных
POSTGRES_USER=логин для подключения к базе данных
POSTGRES_PASSWORD=пароль для подключения к БД
DB_HOST=название сервиса (контейнера)
DB_PORT=порт для подключения к БД
SECRET_KEY=секретный ключ
```
Запустить docker-compose
```
sudo docker-compose up
```
Выполнить миграции
```
docker-compose exec web python manage.py migrate
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
/api/v1/categories/
```
Получение списка всех жанров:

```
/api/v1/genres/
```

Получение списка всех произведений:

```
/api/v1/titles/
```

