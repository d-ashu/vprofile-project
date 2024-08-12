FROM openjdk:11 AS BUILD_IMAGE
RUN apt-get update && apt-get install -y maven

RUN git clone https://github.com/d-ashu/vprofile-project.git
RUN cd vprofile-project && git checkout docker && install mvn

FROM tomcat:9-jre11
LABEL "project"="Vprofile"
LABEL "Author"="Ashutosh"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war/ usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
