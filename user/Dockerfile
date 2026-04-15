# stage 1 
FROM node:20.20.2-alpine3.23 as builder
WORKDIR /app
COPY package.json .
COPY *.js .
RUN npm install

# stage 2
FROM  node:20.20.2-alpine3.23
WORKDIR /app
EXPOSE 8080
COPY --from=builder /app /app
ENV MONGO=true \
    MONGO_URL="mongodb://mongodb:27017/catalogue" \
    REDIS_URL='redis://redis:6379'
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
RUN chown -R roboshop:roboshop /app
USER roboshop
CMD ["server.js"]
ENTRYPOINT ["node"]

