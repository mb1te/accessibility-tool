FROM python:3
MAINTAINER Vladislav Novikov

ENV PYTHONBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

COPY . /backend
WORKDIR /backend

RUN pip install -U pip --quiet && \
    pip install poetry --quiet && \
    poetry config virtualenvs.create false && \
    poetry install --no-dev --quiet

ARG SECRET_KEY=$SECRET_KEY
ARG POSTGRES_USER=$POSTGRES_USER
ARG POSTGRES_PASSWORD=$POSTGRES_PASSWORD
ARG POSTGRES_DB=$POSTGRES_DB

CMD poetry run python manage.py makemigrations && \
    poetry run python manage.py migrate && \
    gunicorn -b 0.0.0.0:8000 --worker-class=gevent --worker-connections=1000 --workers=5 backend.wsgi
