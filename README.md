# Описание проекта YaMDb

Проект YaMDb - это сообщество, где каждый может разместить отзывы (Review) на произведения (Titles). Произведения могут быть разных категории: “Музыка”, “Фильмы”, “Книги”. Список категорий (Category) может быть расширен администратором. 

Каждому новому произведению можно присвоить жанр (Genre) из списка предустановленных в интерфейсе. Так же у администратора есть возможность создавать новые жанры. 

Подробнее об опции Отзыв (Review), которые пользователи могут оставить произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усредненная оценка произведения - рейтинг (целое число) На одно произведение пользователь может оставить только один отзыв и одну оценку. 

Так же есть возможность работать с севисом через API, без использования веб интерфейса.
## Шаблон файла окружения(.env)
```
DB_ENGINE=
DB_NAME=
POSTGRES_USER=
POSTGRES_PASSWORD=
DB_HOST=
DB_PORT=
```
## Запуск приложения:

Клонировать репозиторий и перейти в него в командной строке:

```bash
git clone git@github.com:Zhmurik/infra_sp2.git
```

Создать Docker image и запустить

```bash
docker-compose up -d --build
```

## Управление приложением в контейнере

### Подготовка к запуску приложения
Выполнить миграции базы данных
```bash
docker-compose exec web python manage.py migrate
```

Создать супер пользователя
```bash
docker-compose exec web python manage.py createsuperuser
```

Собрать статические файлы
```bash
docker-compose exec web python manage.py collectstatic --no-input
```
### Импорт данных

Данные в базу данных можно импортирвать из csv-файлов, находящихся в директории api_yamdb/static/data.  
Для импорта в базу данных из файла <file_name>.csv выполните команду:

```bash
docker-compose exec web python manage.py import <file_name>
```

Для импорта в базу данных из всех файлов сразу выполните команду:

```bash
docker-compose exec web python manage.py import all
```

## Образ проекта на DockerHub

Скачать проект из DockerHub 
```bash
docker pull azhmurkova/api_yamdb:latest
```

##

![buld status](https://github.com/zhmurik/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)