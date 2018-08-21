FROM node

# work directory
ADD . /usr/src/server
WORKDIR /usr/src/server

# delete artifacts
RUN rm -rf node_modules build

# install dependencies
RUN npm install -g truffle
RUN npm install --loglevel=warn

# wait for ganache and migrate contracts
RUN ["chmod", "+x", "/usr/src/server/scripts/wait_for_ganache.sh"]
ENTRYPOINT ["/usr/src/server/scripts/wait_for_ganache.sh"]

