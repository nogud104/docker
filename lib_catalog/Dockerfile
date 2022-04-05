FROM python:3.8-slim-buster

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV PYTHONPATH /app:$PYTHONPATH

RUN pip install --upgrade pip --no-cache-dir
COPY ./lib_catalog/requirements.txt /requirements.txt

RUN apt-get update \
    && apt-get install -y --no-install-recommends gcc libc-dev python3-dev \
    && pip install --no-cache-dir -r /requirements.txt

RUN mkdir /app
COPY ./lib_catalog /app

WORKDIR /app

RUN chmod +x /app/entrypoint.sh
RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app

USER appuser
EXPOSE 8000

ENTRYPOINT ["./entrypoint.sh"]