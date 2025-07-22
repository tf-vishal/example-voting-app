FROM python:slim-bookworm

RUN apt-get update && apt-get install -y \
    apache2-utils \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /seed

COPY . /seed

RUN python3 make-data.py

CMD ["/seed/generate-votes.sh"]