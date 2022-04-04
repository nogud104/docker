FROM python:3.7-alpine as base
ENV PYTHONDONTWRITEBYTEapp 1

COPY ./lib_catalog/requirements.txt /app/
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
    libxslt-dev \
    libjpeg-turbo

RUN python -m pip install --no-cache-dir -r /app/requirements.txt


FROM python:3.7-alpine

ENV PYTHONDONTWRITEBYTEapp=1
ENV PYTHONUNBUFFERED=1
ENV PYTHONPATH /app:$PYTHONPATH

WORKDIR /app

COPY --from=base /usr/local/lib/python3.7/site-packages/ /usr/local/lib/python3.7/site-packages/
COPY --from=base /usr/local/bin/ /usr/local/bin/
COPY ./lib_catalog/ /app/

RUN adduser -u 5678 --disabled-password --gecos "" appuser && chown -R appuser /app
USER appuser

EXPOSE 8000

CMD ["gunicorn", "--bind", "0.0.0.0:8000", "lib_catalog.wsgi"]


