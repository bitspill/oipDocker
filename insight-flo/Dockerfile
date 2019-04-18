FROM node:latest

WORKDIR /flocore
RUN npm install -g flocore-node
RUN flocore-node create mynode
RUN cd mynode
RUN flocore-node install flosight-api
RUN flocore-node install flosight-ui

EXPOSE 3001
CMD [ "flocore-node", "start" ]
