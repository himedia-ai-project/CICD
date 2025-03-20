FROM openjdk:17-jdk-slim as builder

WORKDIR /app

COPY gradlew gradlew
COPY gradle gradle
COPY build.gradle build.gradle
COPY settings.gradle settings.gradle

RUN ./gradlew --no-daemon dependencies

COPY . .

RUN chmod +x gradlew

RUN ./gradlew --no-daemon bootJar

FROM openjdk:17-jdk-slim

WORKDIR /app

COPY --from=builder /app/build/libs/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
