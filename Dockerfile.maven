FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app

COPY . .
RUN mvn clean package -DskipTests

FROM openjdk:17-jdk-slim
WORKDIR /app

COPY --from=build /app/target/*.jar /app/app.jar
ENV APP_ARGS "-Dspring.config.location=/app/conf/application.yml -Dservice.config.file=/app/conf/application.yml -Dlogging.config=/app/conf/logback.xml"

EXPOSE 8080
CMD java $JAVA_OPTS $APP_ARGS -jar /app/app.jar