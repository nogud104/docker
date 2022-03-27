
# docker pull postgres
# docker network create --driver bridge --subnet 172.19.0.0/16 --ip-range 172.19.0.0/16 task-bridge-network
# docker run --name database -p 5432:5432 -e POSTGRES_USER=django -e POSTGRES_PASSWORD=django -e POSTGRES_DB=django -d postgres 
# docker network connect --link postgres task-bridge-network database
# docker network connect --link django task-bridge-network django
# docker exec django python manage.py migrate --noinput

FROM python:3
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
WORKDIR /code
COPY requirements.txt /code/
RUN pip install -r requirements.txt
COPY . /code/

EXPOSE 8000

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]