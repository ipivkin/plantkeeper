FROM gradle:jdk17-alpine AS build
COPY --chown=gradle:gradle . /home/gradle/src
WORKDIR /home/gradle/src
RUN gradle buildFatJar --no-daemon

FROM azul/zulu-openjdk:17
EXPOSE 8080:8080
RUN mkdir /app
COPY --from=build /home/gradle/src/build/libs/*.jar /app/plantkeeper.jar
ENTRYPOINT ["java","-jar","/app/plantkeeper.jar"]