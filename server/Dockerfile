FROM node:8-alpine

# work directory
ADD . /usr/src/server
WORKDIR /usr/src/server

# expose the port
EXPOSE 8545

# install packages quietly
RUN npm install --loglevel=warn
RUN npm install -g truffle

# install bash
RUN apk add --no-cache bash

# run build
RUN rm -rf build
RUN npm run ganache-cli:dev
CMD truffle compile