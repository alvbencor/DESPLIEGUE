FROM node:14

WORKDIR /app

COPY ./package.json .

RUN npm install

EXPOSE 80

CMD [ "node", "server.js"]


