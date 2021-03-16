ARG VERSION

#
# Build stage
#
FROM maven:3.6.0-jdk-11-slim AS build
COPY docker-build/pogo /opt/pogo
WORKDIR /opt/pogo/fr.esrf.tango.pogo.parent
RUN mvn clean package

#
# Package stage
#
FROM openjdk:11-jre

RUN apt update && apt install -y libxext6 libxtst6 libxi6 libx11-6 libxrender1

COPY --from=build /opt/pogo/org.tango.pogo.pogo_gui/target/Pogo-9.7.3-SNAPSHOT.jar /usr/local/lib/pogo.jar
ENTRYPOINT ["java","-jar","/usr/local/lib/pogo.jar"]
