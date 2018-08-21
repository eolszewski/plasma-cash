FROM node

# work directory
ADD . /usr/src/server
WORKDIR /usr/src/server

# delete artifacts
RUN rm -rf node_modules build

# install dependencies
RUN npm install -g truffle
RUN npm install --loglevel=warn

# migrate contracts
CMD truffle migrate --network development

