```
# Create an image for the weather-app
FROM node
LABEL org.label-schema.version=v1.1
RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE 3000
CMD ./bin/www
```

```
docker image build -t linuxacademy/weather-app:v1 .
docker image ls
docker container run -d --name weather-app1 -p 8081:3000 linuxacademy/weather-app:v1
docker container ls
```

V2
```
--env [KEY]=[VALUE]
ENV [KEY]=[VALUE]  
ENV [KEY] [VALUE]

# Create an image for the weather-app
FROM node
LABEL org.label-schema.version=v1.1
ENV NODE_ENV="development"
ENV PORT 3000

RUN mkdir -p /var/node
ADD src/ /var/node/
WORKDIR /var/node
RUN npm install
EXPOSE $PORT
CMD ./bin/www
```

```
docker container run -d --name weather-dev -p 8082:3001 --env PORT=3001 linuxacademy/weather-app:v2
docker container run -d --name weather-app2 -p 8083:3001 --env PORT=3001 --env NODE_ENV=production linuxacademy/weather-app:v2
docker container run -d --name weather-prod -p 8084:3000 --env NODE_ENV=production linuxacademy/weather-app:v2
```
