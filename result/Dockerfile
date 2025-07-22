FROM node:24.4.1-slim

RUN apt-get update && apt-get install -y \
    curl tini \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

RUN npm install -g nodemon

COPY . /app

RUN npm install

ENV PORT=80
EXPOSE 80

ENTRYPOINT ["/usr/bin/tini", "--"]
CMD ["node", "server.js"]   