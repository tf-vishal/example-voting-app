#base
#dependencies
#port
#EntryPoint
    

FROM node:24-bullseye-slim

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    curl \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /usr/local/app

RUN npm install -g nodemon

COPY package.json ./
COPY package-lock.json ./

# Install dependencies
RUN npm ci && \
    npm cache clean --force && \
    mv /usr/local/app/node_modules /node_modules

COPY . .

ENV PORT=80
EXPOSE 80

ENTRYPOINT ["/usr/bin/tin1", "--"]
CMD ["node", "server.js"]
