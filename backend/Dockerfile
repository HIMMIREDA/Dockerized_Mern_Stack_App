FROM node:latest

WORKDIR /app

COPY ./package.json ./package-lock.json ./

RUN npm install

COPY ./ ./

EXPOSE 80

RUN chmod 777 /app/logs

CMD ["npm","start"]