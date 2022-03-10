FROM python:3

ENV PYTHONBUFFERED 1
ENV PYTHONDONTWRITEBYTECODE 1

COPY . /backend
WORKDIR /backend

RUN pip install -U pip setuptools --quiet && \
    pip install -r requirements.txt

ARG SECRET_KEY=$SECRET_KEY
ARG POSTGRES_USER=$POSTGRES_USER
ARG POSTGRES_PASSWORD=$POSTGRES_PASSWORD
ARG POSTGRES_DB=$POSTGRES_DB

CMD python manage.py makemigrations && \
    python manage.py migrate && \
    gunicorn -b 0.0.0.0:8000 --worker-class=gevent --worker-connections=1000 --workers=5 backend.wsgi
