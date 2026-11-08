FROM python:3.12.1-slim

# Установка системных зависимостей для psycopg2
RUN apt-get update \
    && apt-get install -y --no-install-recommends gcc libpq-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt /app/
RUN pip install --no-cache-dir -r /app/requirements.txt

COPY app.py /app/
WORKDIR /app

CMD ["uvicorn", "app:app", "--host", "0.0.0.0"]