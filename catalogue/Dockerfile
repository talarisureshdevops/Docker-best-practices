# stage 1 build stage → dependencies install
# source code | node_modules | build tools | cache files | 
# అన్నీ final image లో ఉంటాయి ❌ (size పెద్దది)
FROM node:20.20.2-alpine3.23 as builder
WORKDIR /app
COPY package.json .
COPY *.js .
RUN npm install

# stage 2 final stage → only required files copy | only runtime files (app + required modules)|
# size = చిన్నది (~100MB లేదా ఇంకా తక్కువ)
FROM node:20.20.2-alpine3.23
WORKDIR /app
EXPOSE 8080
COPY --from=builder /app /app
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
RUN chown -R roboshop:roboshop /app
USER roboshop
CMD [ "server.js" ]
ENTRYPOINT [ "node" ]


