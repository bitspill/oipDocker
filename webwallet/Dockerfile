FROM node:alpine

RUN apk add --no-cache git

RUN git clone https://github.com/oipwg/oip-hdmw-interface /usr/src/webwallet
WORKDIR /usr/src/webwallet
RUN npm install

EXPOSE 7000
CMD [ "npm", "start" ]