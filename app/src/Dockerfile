FROM python:3.7-alpine as base

FROM base AS dependencies

WORKDIR /install

RUN apk add --no-cache gcc musl-dev linux-headers
COPY requirements.txt /requirements.txt
RUN pip install --prefix=/install -r /requirements.txt



FROM base

COPY --from=dependencies /install /usr/local

WORKDIR /app
COPY . .

ENV FLASK_APP app.py
ENV FLASK_RUN_HOST 0.0.0.0
ENV REDIS_HOST "redis"
ENV REDIS_PORT "6379"
ENV REDIS_PASSWORD ""

EXPOSE 5000

CMD ["flask", "run"]
