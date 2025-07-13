#Base ImagE?
#Install some tools?
#where does code live ?
#Command to run


FROM python:3.14.0b4-slim

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    apache2-utils \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /seed

COPY . .

#Create POST data files with ab friendly formats
RUN python make-data.py

CMD ["/seed/generate-votes.sh"]