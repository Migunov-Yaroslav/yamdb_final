![example event parameter](https://github.com/Migunov-Yaroslav/yamdb_final/actions/workflows/main.yml/badge.svg?event=push)

# Стек технологий
<p>
  <a 
  target="_blank" href="https://www.python.org/downloads/" title="Python version"><img src="https://img.shields.io/badge/python-_3.7-green.svg">
  </a>
  <a 
  target="_blank" href="https://www.djangoproject.com/download/" title="Django Framework"><img src="https://img.shields.io/badge/django-2.2-green.svg">
  </a>
  <a 
  target="_blank" href="https://www.django-rest-framework.org/" title="Django REST Framework"><img src="https://img.shields.io/badge/DRF-3.12-green.svg">
  </a>
  <a 
  target="_blank" href="https://django-filter.readthedocs.io/en/stable/" title="Django-filter"><img src="https://img.shields.io/badge/django--filter-21.1-green.svg">
  </a>
  <a 
  target="_blank" href="https://django-rest-framework-simplejwt.readthedocs.io/en/stable/" title="JWT"><img src="https://img.shields.io/badge/DRF--SimpleJWT-5.2-green.svg">
  </a>
</p>

# Проект YaMDb_final

Проект YaMDb_final собирает отзывы пользователей на произведения. 
Произведения делятся на категории: «Книги», «Фильмы», «Музыка». 
В каждой категории есть произведения: книги, фильмы или музыка. 
Произведению может быть присвоен жанр. Новые жанры может создавать только 
администратор. Пользователи могут оставить к произведениям текстовые отзывы и 
поставить произведению оценку в диапазоне от одного до десяти. Из 
пользовательских оценок формируется усреднённая оценка произведения — рейтинг. 
Присутствует возможность комментирования отзывов.

Функционал API:
1) Просмотр произведений (кино, музыка, книги), которые подразделяются по жанрам
и категориям.
2) Возможность оставлять отзывы на произведения и ставить им оценки, на основе 
которых построена система рейтингов.
3) Комментирование оставленных отзывов.

Проект разработан командой из трех человек с использованием Git в рамках 
учебного курса Яндекс.Практикум.

## Эндпойнты.
Проект настроен для развертывания на сервере 158.160.21.86. Для использования на
другом сервере или домашнем компьютере необходимо откорректировать следующие 
файлы проекта, указав соответствующие IP адрес и порт:
- yamdb_final/infra/docker-compose.yaml
- yamdb_final/infra/nginx/default.conf

#
Корневой эндпойнт, содержит список ссылок на доступные ресурсы:
```zsh
158.160.21.86/api/v1/
```

Эндпойнт для аутентификации:
```zsh
158.160.21.86/api/v1/auth/signup/
```

Эндпойнт для получения токена:
```zsh
158.160.21.86/api/v1/auth/token/
```

Список пользователей:
```zsh
158.160.21.86/api/v1/users/
```

Список произведений:
```zsh
158.160.21.86/api/v1/titles/
```

Список категорий:
```zsh
158.160.21.86/api/v1/categories/
```

Список жанров:
```zsh
158.160.21.86/api/v1/genres/
```

Документация:
```zsh
158.160.21.86/redoc/
```

## Шаблон наполнения файла .env
Файл .env находится по адресу yamdb_final/infra/. Пример наполнения:
```
DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=*Your password here* # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД
SECRET_KEY=*Your secret_key here* # секретный ключ
```

## Установка проекта запуск в контейнере:

Клонируйте проект себе на локальную машину:
```zsh
sudo git clone https://github.com/Migunov-Yaroslav/yamdb_final.git
```

Перейдите в папку /yamdb_final/infra:
```zsh
cd infra_sp2/infra/
```

Соберите контейнеры:
```zsh
sudo docker-compose up -d --build
```

Примените миграции:
```zsh
sudo docker-compose exec web python manage.py migrate
```

При необходимости создайте суперпользователя:
```zsh
sudo docker-compose exec web python manage.py createsuperuser
```

Соберите статику:
```zsh
sudo docker-compose exec web python manage.py collectstatic --no-input
```

При необходимости импортируйте тестовые данные в БД:
```zsh
sudo docker-compose exec web python manage.py import_data_from_csv
```

Проект доступен по адресу:
[158.160.21.86/api/v1/](http://158.160.21.86/api/v1/)

Разработчики:
```zsh
1. Кирилл Марин (https://github.com/MilkaMjoy):
Разработка системы регистрации и аутентификации, прав доступа, работы с токеном, 
системы подтверждения через e-mail.

2. Ярослав Мигунов (https://github.com/Migunov-Yaroslav):
Разработка моделей "категории" (Categories), "жанры" (Genres) и "произведения" 
(Titles), а также разработка представлений и эндпойнтов для них. Контейнеризация 
проекта. Настройка  Git Actions.

3. Людмила Давлетова (https://github.com/luydmila-davletova):
Разработка моделей "отзывы" (Review) и "комментарии" (Comments), а также 
разработка представлений и эндпойнтов для них. Настройка прав доступа для 
запросов. Реализация системы рейтингов.
```
