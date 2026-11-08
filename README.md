# Лабораторная работа №1. Управление многоконтейнерными системами

**Дисциплина:** Непрерывное интегрирование и сборка программного обеспечения (НиИСПО)  
**Студент:**  Мирзаев Эмин Парвизович
**Группа:** 13  
**Год:** 2026

\---

## 📖 О работе

Лабораторная работа посвящена изучению современных технологий контейнеризации:

* Docker Engine и Docker Desktop
* Dockerfile и многоэтапная сборка (multi-stage builds)
* Оптимизация Docker-образов
* Docker Compose и многоконтейнерные инфраструктуры

\---

## 🚀 Как запустить

### Задание 1. Nginx с монтированием HTML

```bash
cd task1
docker run -d --name mynginx -p 8081:80 -v ${PWD}:/usr/share/nginx/html nginx:alpine
# Открыть http://localhost:8081
```

### Задание 2. Свой образ

```bash
cd task2
docker build -t mynginx-custom:v1 .
docker run -d --name mynginx-custom -p 8083:80 mynginx-custom:v1
# Открыть http://localhost:8083
```

### Задание 3. Python + PostgreSQL

```bash
# 1. Запустить PostgreSQL
docker run --name postgres-db \\
  -e POSTGRES\_PASSWORD=apipass \\
  -e POSTGRES\_DB=api \\
  -e POSTGRES\_USER=apiuser \\
  -p 5432:5432 -d postgres:16.2-alpine

# 2. Собрать и запустить приложение (любую версию v1–v6)
cd task3/simple\_python\_app
docker build -t simple\_python\_app:v6 -f Dockerfile.v6 .
docker run --rm -p 8001:8000 \\
  -e API\_DB\_HOST=host.docker.internal \\
  simple\_python\_app:v6
# Открыть http://localhost:8001
```

### Задание 4. Docker Compose

```bash
cd task4/compose
docker compose up -d
# Открыть http://localhost
docker compose down -v
```

