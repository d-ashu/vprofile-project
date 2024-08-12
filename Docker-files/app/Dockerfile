# Stage 1: Build the project with Maven
FROM openjdk:11 AS build_image
RUN apt-get update && apt-get install -y maven git

# Clone the repository
RUN git clone https://github.com/d-ashu/vprofile-project.git

# Switch to the correct branch and build the project
RUN cd vprofile-project && git checkout docker && mvn clean install

# Stage 2: Set up Tomcat and deploy the WAR file
FROM tomcat:9-jre11
LABEL "project"="Vprofile"
LABEL "Author"="Ashutosh"

# Remove the default webapps
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy the WAR file from the build stage to Tomcat's webapps directory
COPY --from=build_image /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose port 8080
EXPOSE 8080

# Start Tomcat
CMD ["catalina.sh", "run"]
