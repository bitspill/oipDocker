FROM node:8

WORKDIR /flocore
RUN npm install flocore-node
RUN ./node_modules/flocore-node/bin/flocore-node create mynode
RUN cd mynode
RUN ./node_modules/flocore-node/bin/flocore-node install flosight-api
RUN ./node_modules/flocore-node/bin/flocore-node install flosight-ui

EXPOSE 3001
CMD [ "flocore-node", "start" ]
