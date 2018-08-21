FROM node
RUN npm install -g ganache-cli@6.1.0
EXPOSE 8545
COPY ganache-cli.sh /usr/src/ganache/ganache-cli.sh
RUN ["chmod", "+x", "/usr/src/ganache/ganache-cli.sh"]
ENTRYPOINT ["/usr/src/ganache/ganache-cli.sh"]