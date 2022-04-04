# FROM python:3.8-slim-buster as base
# ENV PYTHONDONTWRITEBYTECODE 1

# COPY ./lib_catalog/requirements.txt /code/
# RUN apk add --update --no-cache --virtual .build-deps \
#     && apk add postgresql-dev gcc python3-dev musl-dev

# RUN pip install --no-cache-dir -r /code/requirements.txt 
# COPY . /code/


# FROM python:3.8-slim-buster

# ENV PYTHONDONTWRITEBYTECODE=1
# ENV PYTHONUNBUFFERED=1
# ENV PYTHONPATH /code:$PYTHONPATH

# WORKDIR /code

# COPY --from=base /usr/local/lib/python3.7/site-packages/ /usr/local/lib/python3.7/site-packages/
# COPY --from=base /usr/local/bin/ /usr/local/bin/
# COPY ./lib_catalog/ /code/

# RUN chmod +x /code/entrypoint.sh
# RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /code

# USER appuser

# EXPOSE 8000

FROM python:3.8-slim-buster

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
ENV PYTHONPATH /app:$PYTHONPATH

RUN pip install --upgrade pip --no-cache-dir
COPY ./lib_catalog/requirements.txt /requirements.txt
# packages required for setting up WSGI
RUN apt-get update \
    && apt-get install -y --no-install-recommends gcc libc-dev python3-dev \
    && pip install --no-cache-dir -r /requirements.txt

RUN mkdir /app
COPY ./lib_catalog /app

WORKDIR /app

RUN chmod +x /app/entrypoint.sh
RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app

USER appuser

CMD ["entrypoint.sh"]