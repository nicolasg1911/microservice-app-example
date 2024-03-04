
<h1>Workshop 6</h1>
<h2>beginnig</h2>
    <p>I started by reading the readme of each microservice to start building the dockerfile for launching one by one</p>
<h2>Users API</h2>
    <p>by reading the microservices readme I build the dockerfile like this:
       FROM openjdk:8-jdk
       WORKDIR /usr/src/app
       COPY . .
       RUN ./mvnw clean install
       ENV SPRING_ZIPKIN_BASE_URL=http://zipkin:9411 
       ENV JWT_SECRET=PRFT
       ENV SERVER_PORT=8083
       EXPOSE $SERVER_PORT
       CMD ["java", "-jar", "target/users-api-0.0.1-SNAPSHOT.jar"]
       Getting the library then copying the files in the workdir and initializing Environment variables such as the zipkin URL and the port and finally executing 
    </p>

<h2>Log Message</h2>
    <p>FROM python:3.6
       WORKDIR /app
       COPY . .
       RUN pip3 install -r requirements.txt
       EXPOSE 6029
       ENV REDIS_HOST=redis
       ENV REDIS_PORT=6379 
       ENV REDIS_CHANNEL=log_channel 
       CMD ["python3", "main.py"]
       Getting the library then copying the files in the workdir, setting the listening port and initializing Environment variables such as the redis host and its port and finally executing 
    </p>

<h2>Frontend</h2>
    <p>FROM node:9.11.1-alpine as build-stage
       WORKDIR /app
       COPY . .
       RUN npm install
       RUN npm run build
       ENV PORT=8080
       EXPOSE 8080
       ENV AUTH_API_ADDRESS=http://authapi:8000
       ENV TODOS_API_ADDRESS=http://todosapi:8082
       CMD ["npm", "start"]
       Getting the library then copying the files in the workdir, installing and running npm, setting the listening port and initializing Environment variables such as the Auth API address and the To Dos API address and finally executing 
    </p>

<h2>Auth API</h2>
    <p>FROM golang:1.22
       WORKDIR /usr/src/app
       COPY . .
       ENV GO111MODULE=on
       RUN go mod init github.com/bortizf/microservice-app-example/tree/master/auth-api
       RUN go mod tidy
       RUN go build
       EXPOSE 8000
       ENV JWT_SECRET=PRFT
       ENV AUTH_API_PORT=8000
       ENV USERS_API_ADDRESS=http://usersapi:8083
       CMD ["./auth-api"]
       Getting the library then copying the files in the workdir, setting the go module on, running the proyect mods, setting the listening port and initializing Environment variables such as the Auth API address and the Users API address and finally executing 
    </p>

<h2>ToDos API</h2>
    <p>FROM node:8.17.0
       WORKDIR /app
       COPY . .
       RUN npm install
       ENV AUTH_API_ADDRESS=http://authapi:8000
       ENV TODOS_API_ADDRESS=http://todosapi:8082
       ENV TODO_API_PORT=8082
       ENV JWT_SECRET=PRFT
       ENV REDIS_HOST=redis
       ENV REDIS_PORT=6379
       ENV REDIS_CHANNEL=log_channel
       EXPOSE ${TODO_API_PORT}
       CMD ["npm", "start"]
       Getting the library then copying the files in the workdir, installing npm dependencies, initializing Environment variables such as the Auth API address, the To Dos API address and the redis host then finally executing 
    </p>


