FROM python:3.10-slim
ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /
RUN useradd -u 1000 -m app

RUN apt-get update && \
  apt-get install -y --no-install-recommends \
  build-essential \
  gcc \
  libssl-dev \
  libffi-dev \
  libpcre3-dev \
  && pip install --no-cache-dir pipenv \
  && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /var/www/app && mkdir /app

COPY Pipfile* /app
RUN cd /app && pipenv install --system --deploy

COPY . /app

CMD uwsgi --http :5000 --master --enable-threads -s /var/www/app/app.sock --manage-script-name --mount /=app:app
