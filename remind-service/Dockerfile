FROM openjdk:8u181-jdk-alpine3.8
ADD ["target/remind-service.jar", "app.jar"]
EXPOSE 8080

# Change TimeZone
RUN apk add --update tzdata
ENV TZ=Asia/Ho_Chi_Minh

# Clean APK cache
RUN rm -rf /var/cache/apk/*

ENV DATABASE_HOST=localhost
ENV DATABASE_NAME=remindapp
ENV DATABASE_PORT=27017
ENV DATABASE_USER=root
ENV DATABASE_PASSWORD=example
ENV DATABASE_URL=mongodb://${DATABASE_USER}:${DATABASE_PASSWORD}@${DATABASE_HOST}:${DATABASE_PORT}/${DATABASE_NAME}
ENV SPRING_ENV=development


ENV JAVA_OPTS="-Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8787,suspend=n"
RUN sh -c 'touch /app.jar'
ENTRYPOINT [ "sh", "-c", "java $JAVA_OPTS -Djava.security.egd=file:/dev/./urandom -Dspring.profiles.active=$SPRING_ENV -jar /app.jar --database.url=$DATABASE_URL --database.host=$DATABASE_HOST --database.port=$DATABASE_PORT --database.user=$DATABASE_USER --database.password=$DATABASE_PASSWORD --database.name=$DATABASE_NAME" ]
