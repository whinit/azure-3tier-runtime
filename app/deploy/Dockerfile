# build stage
FROM eclipse-temurin:21-jdk-jammy AS builder
WORKDIR /app
COPY . .
RUN chmod +x gradlew
RUN ./gradlew build

# run stage
FROM eclipse-temurin:21-jre-jammy AS runner
ENV PROFILE "dev"
ENV MYSQL_HOST "localhost"
ENV DB_USERNAME "user"
ENV DB_PASSWORD "password"
ENV DB_NAME "library"
ENV REDIS_HOST "localhost"
ENV REDIS_PORT "6379"

EXPOSE 8080

WORKDIR /app
COPY --from=builder /app/build/libs/*.jar ./app.jar
COPY --from=builder /app/deploy/start-server.sh ./start-server.sh
RUN chmod +x /app/start-server.sh

ENTRYPOINT /app/start-server.sh
