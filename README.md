# yamdb_final
Итоговое задание - Проект: CI и CD проекта api_yamdb

![example workflow](https://github.com/usdocs/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

[Путь до API](http://178.154.205.59/api/v1/)

[Документация API](http://178.154.205.59/redoc/)

## Описание

Проект YaMDb собирает отзывы пользователей на произведения. Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
Произведения делятся на категории, такие как «Книги», «Фильмы», «Музыка». Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Жуки» и вторая сюита Баха. Список категорий может быть расширен (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»). 
Произведению может быть присвоен жанр из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). 
Добавлять произведения, категории и жанры может только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.
Пользователи могут оставлять комментарии к отзывам.
Добавлять отзывы, комментарии и ставить оценки могут только аутентифицированные пользователи.

#### Доступный функционал

- Для аутентификации используются JWT-токены.
- У неаутентифицированных пользователей доступ к API только на уровне чтения.
- Создание объектов разрешено только аутентифицированным пользователям.На прочий фунционал наложено ограничение в виде административных ролей и авторства.
- Управление пользователями.
- Получение списка всех категорий и жанров, добавление и удаление.
- Получение списка всех произведений, их добавление.Получение, обновление и удаление конкретного произведения.
- Получение списка всех отзывов, их добавление.Получение, обновление и удаление конкретного отзыва.  
- Получение списка всех комментариев, их добавление.Получение, обновление и удаление конкретного комментария.
- Возможность получения подробной информации о себе и удаления своего аккаунта.
- Фильтрация по полям.

## Стек технологий:
- Python 3
- DRF (Django REST framework)
- Django ORM
- Docker
- Gunicorn
- nginx
- Яндекс Облако(Ubuntu 18.04)
- Django 3.2
- PostgreSQL
- GIT

## Шаблон наполнения .env
```
# указываем, с какой БД работаем
DB_ENGINE=django.db.backends.postgresql
# имя базы данных
DB_NAME=
# логин для подключения к базе данных
POSTGRES_USER=
# пароль для подключения к БД
POSTGRES_PASSWORD=
# название сервиса (контейнера)
DB_HOST=
# порт для подключения к БД
DB_PORT=
# секретный ключ Django
SECRET_KEY=
```

## Автоматизация развертывания серверного ПО
Для автоматизации развертывания ПО на боевых серверах используется среда виртуализации Docker, а также Docker-compose - инструмент для запуска многоконтейнерных приложений. Docker позволяет «упаковать» приложение со всем его окружением и зависимостями в контейнер, который может быть перенесён на любую Linux -систему, а также предоставляет среду по управлению контейнерами. Таким образом, для разворачивания серверного ПО достаточно чтобы на сервере с ОС семейства Linux были установлены среда Docker и инструмент Docker-compose.

## Описание команд для запуска приложения в контейнерах
Для запуска проекта в контейнерах используем **docker-compose** : ```docker-compose up -d --build```, находясь в директории (infra) с ```docker-compose.yaml```

После сборки контейнеров выполяем:
```bash
# Выполняем миграции
docker-compose exec web python manage.py migrate
# Создаем суперппользователя
docker-compose exec web python manage.py createsuperuser
# Собираем статику со всего проекта
docker-compose exec web python manage.py collectstatic --no-input
```

#### Примеры некоторых запросов API

Регистрация пользователя:  
``` POST /api/v1/auth/signup/ ```  
Получение данных своей учетной записи:  
``` GET /api/v1/users/me/ ```  
Добавление новой категории:  
``` POST /api/v1/categories/ ```  
Удаление жанра:  
``` DELETE /api/v1/genres/{slug}/ ```  
Частичное обновление информации о произведении:  
``` PATCH /api/v1/titles/{titles_id}/ ```  
Получение списка всех отзывов:  
``` GET /api/v1/titles/{title_id}/reviews/ ```   
Добавление комментария к отзыву:  
``` POST /api/v1/titles/{title_id}/reviews/{review_id}/comments/ ```    

#### Полный список запросов API находятся в документации

#### Авторы
- Андрей Балакин
- Михаил Волков
- Павел Марычев
