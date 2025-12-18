<h1 align="center" style="display: block; font-size: 2.5em; font-weight: bold; margin-block-start: 1em; margin-block-end: 1em;">
  <a name="logo">
    <img src="pictures/icon.png" alt="URL Inspector" style="width:350px;height:350px"/>
  </a>
  <br /><br />
  <strong>URL-INSPECTOR</strong>
</h1>

<div align="center">

![FastAPI](https://img.shields.io/badge/FastAPI-009688?logo=fastapi&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?logo=redis&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?logo=mongodb&logoColor=white)

</div>

<p align="center">
  <em>URL Inspector — это сервис для анализа и проверки ссылок.<br />
  Он позволяет получать <b>HTTP статус-коды</b>, проверять <b>SSL</b>, отслеживать <b>редиректы</b>,<br />
  извлекать <b>заголовки и мета-теги</b>, а также сохранять результаты в <b>MongoDB</b>.</em>
</p>


## Содержание
- [Быстрый старт](быстрый-старт)
- [Docker](#docker)
- [Стек технологий](#стек-технологий)
- [Функциональность](#функциональность)
- [Архитектура проекта](#архитектура-проекта)
- [Примеры использования](#примеры-использования)
- [TODO](#todo)


## Быстрый старт
1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/username/url-inspector.git

   cd url-inspector

   pip install -r requirements.txt
   ```
2. Создайте файл .env в корне проекта и укажите параметры окружения:
    ```bash
    MONGO_URL = "mongodb://localhost:27017"
    MONGO_DB = "url_inspector"
    REDIS_URL = "redis://localhost:6379"
    ```
3. Запустите Redis - его можно поднять локально или через Docker:
    ```bash
    # Локальный запуск (если Redis уже установлен)
    redis-server

    # Или через Docker
    docker run -d --name redis -p 6379:6379 redis
    ```
4. Запустите прилоежние:
    ```bash
    uvicorn app.main:app --reload
    ```

## Docker
Если хочешь быстро поднять весь проект вместе с зависимостями, используй Docker Compose:
```bash
docker-compose up --build
```
Контейнер автоматически развернет:
- FastAPI-приложение;
- Redis для кэша и очередей;
- MongoDB для хранения данных;

После сборки серевис будет досутпен по адресу `http://localhost:8000`.

## Стек технологий
Проект построен на современных инструментах для асинхронного бэкенда:

- `FastAPI` - основной веб-фреймворк;
- `MongoDB` - база данных для хранения результатов анализа;
- `Redis` - кэш и брокер фоновых задач;
- `aiohttp` / `httpx` - асинхронные HTTP-запросы
- `Uvicorn` - ASGI-сервер для запуска приложения;
- `Docker` - контейнеризация и простая сборка окружения.

## Функциональность
- Проверка HTTP-статуса и времени ответа;
- Анализ SSL-сертификата (действительность, срок, организация);
- Отслеживание редиректов;
- Извлечение мета-тегов (title, description, keywords);
- Сохранение результатов анализа в MongoDB;
- Асинхронная обработка запросов через FastAPI;
- Очередь задач с Redis для параллельной проверки множества ссылок.

## Архитектура проекта
```bash
url-inspector/
├── app/
│   ├── repositories/           # Работа с базами данных и кэшом
│   │   ├── database.py         # Подключение и функции для MongoDB
│   │   └── redis_cache.py      # Работа с Redis (кэш и задачи)
│   │
│   ├── routing/                # Основные роуты FastAPI
│   │   ├── analyze.py          # Проверка и анализ ссылок
│   │   ├── history.py          # История проверок
│   │   └── report.py           # Формирование и выдача отчётов
│   │
│   ├── schemas/                # Pydantic-схемы для валидации данных
│   │   ├── analyze.py
│   │   ├── history.py
│   │   └── report.py
│   │
│   ├── services/               # Логика и обработка данных
│   │   ├── report_service.py   # Генерация отчётов и статистики
│   │   └── url_checks.py       # Проверка ссылок, статусов, SSL
│   │
│   ├── config.py               # Конфигурация и загрузка .env
│   ├── depends.py              # Зависимости для DI FastAPI
│   └── main.py                 # Точка входа приложения
│
├── .env.example                # Пример конфигурации окружения
├── docker-compose.yml          # Docker-сборка и контейнеры
├── Dockerfile                  # Образ приложения
├── requirements.txt            # Зависимости Python
└── README.md                   # Документация проекта
```

### Логика слоёв:
- `repositories` - низкоуровневая работа с MongoDB и Redis;
- `services` - бизнес-логика проверки ссылок;
- `schemas` - структура данных для запросов/ответов;
- `routing` - API-эндпоинты FastAPI;
- `config` и `depends` - настройка окружения и зависиммостей.

## TODO
- Добавить экспорт отчетов в PDF и CSV (возможно нет);
- Написать интеграционные тесты;
- Реализовать очередь задч через Celery / RQ;
- Расширить анализ метаданных (Open Graph, favicon);
- Подключить фронтенд-панель (React или Svetle).





