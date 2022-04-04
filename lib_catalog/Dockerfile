FROM python:3.7-alpine as base
ENV PYTHONDONTWRITEBYTECODE 1

COPY ./lib_catalog/requirements.txt /code/
RUN apk add --update --no-cache --virtual .build-deps \
    build-base \
    postgresql-dev \
    libffi-dev \
    python3-dev \
    libffi-dev \
    jpeg-dev \
    zlib-dev \
    musl-dev \
    libpq \
    libxml2-dev \
    libxslt-dev

RUN pip install --no-cache-dir -r /code/requirements.txt 
COPY . /code/


FROM python:3.7-alpine

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PYTHONPATH /code:$PYTHONPATH

WORKDIR /code

COPY --from=base /usr/local/lib/python3.7/site-packages/ /usr/local/lib/python3.7/site-packages/
COPY --from=base /usr/local/bin/ /usr/local/bin/
COPY ./lib_catalog/ /code/

RUN chmod +x /code/entrypoint.sh
RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /code

USER appuser

EXPOSE 8000

ENTRYPOINT [ "/code/entrypoint.sh" ]