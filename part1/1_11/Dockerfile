FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
COPY . .
RUN npm install

EXPOSE 8000
ENTRYPOINT [ "npm", "start" ]
