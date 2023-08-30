# Kittygram
## Учебный проект Замечательные коты
![example workflow](https://github.com/iultina/kittygram_final/actions/workflows/main.yml/badge.svg)

## **Описание проекта**
Этот проект позволит вам выкладывать свои и любоваться чужими фото котов и кошек.
В описание добавьте имя, цвет и достижения пушистого героя.
Красиво и абсолютно безопасно для аллергиков:)


## **Стэк технологий**

* [Python 3.9](https://www.python.org/downloads/)
* [Django 3.2.3](https://www.djangoproject.com/download/)
* [djangorestframework 3.12.4](https://pypi.org/project/djangorestframework/#files)
* [djoser 2.1.0](https://pypi.org/project/djoser/#files)
* [webcolors 1.11.1](https://pypi.org/project/webcolors/1.11.1/)
* [gunicorn 20.1.0](https://pypi.org/project/gunicorn/20.1.0/)
* [psycopg2-binary 2.9.6](https://pypi.org/project/psycopg2-binary/#files)
* [pytest-django 4.4.0](https://pypi.org/project/pytest-django/)
* [pytest-pythonpath 0.7.3](https://pypi.org/project/pytest-pythonpath/)
* [pytest 6.2.4](https://pypi.org/project/pytest/)
* [PyYAML 6.0](https://pypi.org/project/PyYAML/)
* [python-dotenv 1.0.0](https://pypi.org/project/python-dotenv/)

## Локальный запуск проекта

Клонировать репозиторий и перейти в него в командной строке:

```bash
git clone https://github.com/iultina/kittygram_final.git
cd kittygram_final
```

Cоздать и активировать виртуальное окружение, установить зависимости:

```bash
python3 -m venv venv && \ 
    source venv/scripts/activate && \
    python -m pip install --upgrade pip && \
    pip install -r backend/requirements.txt
```

Установите [docker compose](https://www.docker.com/) на свой компьютер.

Запустите проект через docker-compose:

```bash
docker compose -f docker-compose.yml up --build -d
```

Выполнить миграции:

```bash
docker compose -f docker-compose.yml exec backend python manage.py migrate
```

Соберите статику и скопируйте ее:

```bash
docker compose -f docker-compose.yml exec backend python manage.py collectstatic  && \
docker compose -f docker-compose.yml exec backend cp -r /app/static_backend/. /backend_static/static/
```

## .env

В корне проекта создайте файл .env и пропишите в него свои данные.

Пример:

```apache
POSTGRES_DB=kittygram
POSTGRES_USER=kittygram_user
POSTGRES_PASSWORD=kittygram_password
DB_NAME=kittygram
```

## Workflow

Для использования Continuous Integration (CI) и Continuous Deployment (CD): в репозитории GitHub Actions `Settings/Secrets/Actions` прописать Secrets - переменные окружения для доступа к сервисам:

```
SECRET_KEY                     # стандартный ключ, который создается при старте проекта

DOCKER_USERNAME                # имя пользователя в DockerHub
DOCKER_PASSWORD                # пароль пользователя в DockerHub
HOST                           # ip_address сервера
USER                           # имя пользователя
SSH_KEY                        # приватный ssh-ключ (cat ~/.ssh/id_rsa)
PASSPHRASE                     # кодовая фраза (пароль) для ssh-ключа

TELEGRAM_TO                    # id телеграм-аккаунта (можно узнать у @userinfobot, команда /start)
TELEGRAM_TOKEN                 # токен бота (получить токен можно у @BotFather, /token, имя бота)
```

При push в ветку main автоматически отрабатывают сценарии:

* *tests* - проверка кода на соответствие стандарту PEP8 и запуск pytest. Дальнейшие шаги выполняются только если push был в ветку main;
* *build\_and\_push\_to\_docker\_hub* - сборка и доставка докер-образов на DockerHub
* *deploy* - автоматический деплой проекта на боевой сервер. Выполняется копирование файлов из DockerHub на сервер;
* *send\_message* - отправка уведомления в Telegram.

## Автор
Tina Kirilenko 📧 Telegram: @Mi_2018

🔗 LinkedIn: linkedin.com/in/iultina


