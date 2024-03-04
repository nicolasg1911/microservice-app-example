# etapa de compilación
FROM node:9.11.1-alpine as build-stage
WORKDIR /app
COPY . .

RUN npm install
RUN npm run build
ENV PORT=8080
EXPOSE 8080
ENV AUTH_API_ADDRESS=http://authapi:8000
ENV TODOS_API_ADDRESS=http://todosapi:8082
CMD ["npm", "start"]
