# Establecer imagen base
FROM node:14.15.1-alpine

# Instalar http-server de forma global usando npm
RUN npm install -g http-server

# Establecer directorio de trabajo
WORKDIR /app

COPY /src .
COPY /public .

RUN npm install

EXPOSE 8080

CMD ["http-server", "/dist"]