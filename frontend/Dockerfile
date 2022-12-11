FROM node:latest

WORKDIR /app

COPY ./package.json ./package-lock.json ./

RUN npm install

ENV NODE_ENV development

ENV NODE_OPTIONS=--openssl-legacy-provider

COPY ./ ./

EXPOSE 3000

CMD ["npm","start"]