# stage 1
FROM maven:3.9.14 as builder
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn clean package
RUN mv target/*.jar shipping.jar
# stage 2
FROM eclipse-temurin:17-jre-alpine
EXPOSE 8080
ENV CART_ENDPOINT=cart:8080 \
    DB_HOST=mysql
WORKDIR /app
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop && \
    chown -R roboshop:roboshop /app
COPY --from=builder /app/shipping.jar .
USER roboshop
ENTRYPOINT ["java", "-jar", "shipping.jar"]

# added comments regarding the shipping
# FROM maven:3.9.14
# EXPOSE 8080
# WORKDIR /app
# COPY pom.xml .
# COPY src ./src
# RUN mvn clean package
# RUN mv target/shipping-1.0.jar shipping.jar
# ENV CART_ENDPOINT="cart:8080" \
    # DB_HOST="mysql"
# CMD ["java","-jar","shipping.jar"]
