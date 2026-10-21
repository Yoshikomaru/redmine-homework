# Redmine Docker Homework

Домашнее задание по Docker, Volumes.

## Описание

Приложение Redmine с базой данных PostgreSQL.

Используются два контейнера, два Docker volume и отдельная Docker network.

## Сборка и публикация

```bash
docker build -t USERNAME/redmine-homework:1.0 .
docker login
docker push USERNAME/redmine-homework:1.0
```

USERNAME необходимо заменить на логин Docker Hub.

## Запуск

Создать файл `.env` со следующими переменными:

```dotenv
DOCKERHUB_USER=USERNAME
DB_PASSWORD=YOUR_STRONG_PASSWORD
REDMINE_SECRET_KEY_BASE=YOUR_GENERATED_SECRET
```

Запустить приложение:

```bash
docker compose pull
docker compose up -d
```

Проверить:

```bash
docker compose ps
docker volume ls
docker network ls
```

Redmine доступен по адресу:

`http://SERVER_IP:8080`

## Хранение данных

- `postgres-data` — база данных PostgreSQL.
- `redmine-files` — загруженные файлы Redmine.

## Docker network

Сервисы объединены отдельной сетью `redmine-net`.

Порт PostgreSQL наружу не опубликован.

## Остановка

```bash
docker compose down
```

Данные в volumes сохраняются.

Для удаления контейнеров вместе с данными используется `docker compose down -v`. Эта команда удаляет данные и не должна применяться при обычной остановке.
