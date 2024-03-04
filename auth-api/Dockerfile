FROM golang:1.22

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
