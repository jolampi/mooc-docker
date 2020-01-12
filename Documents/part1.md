# Part 1

## 1.1
```
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                          PORTS               NAMES
a4a31b83870a        nginx               "nginx -g 'daemon of…"   2 minutes ago       Up 2 minutes                    80/tcp              wonderful_driscoll
1e8c5e5eaa7b        nginx               "nginx -g 'daemon of…"   2 minutes ago       Exited (0) About a minute ago                       hardcore_rubin
ed738053bab1        nginx               "nginx -g 'daemon of…"   2 minutes ago       Exited (0) About a minute ago                       dreamy_cannon
```

## 1.2
```
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES

REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
```

## 1.3
```
$ docker run -it devopsdockeruh/pull_exercise
> basics
"This is the secret message"
```

## 1.4
```
$ docker run -d --name 1_4 devopsdockeruh/exec_bash_exercise
$ docker exec -it 1_4 bash
$ tail -f ./logs.txt
"Docker is easy"
```

## 1.5
```
$ docker run -d -it --name 1_5 ubuntu sh -c 'echo "Input website:"; read website; echo "Searching.."; sleep 1; curl http://$website;'
$ docker exec 1_5 sh -c 'apt-get update; apt-get -y install curl;'
$ docker attach 1_5
>helsinki.fi
```

## 1.6
```Dockerfile
FROM devopsdockeruh/overwrite_cmd_exercise
CMD ["-c"]
```

## 1.7
#### curler.sh
```bash
#!/bin/bash
echo "Input website:"
read website
echo "Searching.."
sleep 1
curl http://$website
```
#### Dockerfile
```Dockerfile
FROM ubuntu

WORKDIR /exercise
RUN apt-get update && apt-get install -y curl

COPY curler.sh .
RUN chmod +x ./curler.sh
CMD ["./curler.sh"]
```

## 1.8
```
$ touch logs.txt
$ docker run -v $(pwd)/logs.txt:/usr/app/logs.txt devopsdockeruh/first_volume_exercise
```

## 1.9
```
$ docker run -d -p 80 --name ports devopsdockeruh/ports_exercise
$ docker port ports
(browser): https://localhost:32768
```

## 1.10
```Dockerfile
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
COPY . .
RUN npm install

EXPOSE 5000
ENTRYPOINT [ "npm", "start" ]
```

## 1.11
```Dockerfile
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
COPY . .
RUN npm install

EXPOSE 8000
ENTRYPOINT [ "npm", "start" ]
```
```
$ docker run -d -p 8000:8000 -v $(pwd)/logs.txt:/logs.txt backendexample
```

## 1.12
#### Backend Dockerfile
```Dockerfile
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
COPY . .
RUN npm install

ENV FRONT_URL=http://localhost:5000
EXPOSE 8000
ENTRYPOINT [ "npm", "start" ]
```
#### Frontend Dockerfile
```Dockerfile
FROM ubuntu:16.04

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs
COPY . .
RUN npm install

ENV API_URL=http://localhost:8000
EXPOSE 5000
ENTRYPOINT [ "npm", "start" ]
```
```
$ docker run -d -p 8000:8000 backendexample
$ docker run -d -p 5000:5000 frontendexample
```

## 1.13
```Dockerfile
FROM openjdk:8

COPY . .
RUN ./mvnw package

EXPOSE 8080
ENTRYPOINT [ "java", "-jar", "./target/docker-example-1.1.3.jar" ]
```

## 1.14
```Dockerfile
FROM ruby:2.6.0

RUN apt-get update && apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash && apt install -y nodejs

COPY . .
RUN bundle install
RUN rails db:migrate

EXPOSE 3000
ENTRYPOINT [ "rails", "s" ]
```

## 1.15
* https://hub.docker.com/r/jolampi/ultira-ai-toe

## 1.16
* https://docker-exercise-1999.herokuapp.com/
