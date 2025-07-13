# Base
# Copy COde
# Dependencies
# Port 80
# Dev and production commands

#Stage1

FROM python:3.13.5-slim AS base

RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    rm -rf /var/lib/apt/lists/*

COPY requirements.txt /app/requirements.txt
RUN pip install --no-cache-dir -r /app/requirements.txt

#Stage 2 for Dev

FROM base AS dev

RUN pip install watchdog
ENV FLASK_ENV=development
CMD ["python","app.py"]

#stage 3 

FROM base AS final

COPY . .

EXPOSE 80

CMD ["gunicorn", "app:app", "-b", "0.0.0.0:80", "--access-logfile", "-", "--error-logfile", "-", "--workers", "4", "--keep-alive", "0"]
