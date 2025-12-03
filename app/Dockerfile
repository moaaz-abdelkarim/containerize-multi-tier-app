FROM openjdk:26-ea-17-slim AS build
WORKDIR /app
COPY . .
RUN apt update && apt install -y maven
COPY application.properties /app/src/main/resources/application.properties
RUN mvn clean install -DskipTests

FROM tomcat:9-jre11
RUN rm -rf  /usr/local/tomcat/webapps/*  
COPY --from=build /app/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war
RUN useradd -m -u 1011 -s /bin/bash admin_vp
RUN chown admin_vp:admin_vp -R /usr/local/tomcat
USER admin_vp
EXPOSE 8080
CMD ["catalina.sh", "run"] 