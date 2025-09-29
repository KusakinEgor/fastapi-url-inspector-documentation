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


## 📑 Содержание
- ⚡️ [Быстрый старт](#️-быстрый-старт)
- 🐳 [Docker](#-docker)
- 🛠 [Стек технологий](#-стек-технологий)
- 🚀 [Функциональность](#-функциональность)
- 📂 [Архитектура проекта](#-архитектура-проекта)
- 📌 [Примеры использования](#-примеры-использования)
- ✅ [TODO](#-todo)


## ⚡️ Быстрый старт
1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/username/url-inspector.git

   cd url-inspector

   pip install -r requirements.txt

   uvicorn main:app --reload
   ```

