FROM python:slim-bookworm AS builder

RUN apt-get update && apt-get install -y \
    curl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

FROM builder AS dev
RUN pip install watchdog
ENV FLASK_ENV=development
CMD ["python", "app.py"]

FROM builder AS final

COPY . .

EXPOSE 80

CMD ["gunicorn", "-b", "0.0.0.0:80", "app:app", "--workers", "4", "--error-logfile", "-", "--access-logfile", "-", "--keep-alive", "0"]
