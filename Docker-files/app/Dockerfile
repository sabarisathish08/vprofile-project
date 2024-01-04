# Build stage
FROM openjdk:11-jdk AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/sabarisathish08/vprofile-project.git
RUN cd vprofile-project && git checkout docker && mvn install 

# Intermediate stage for copying files
FROM openjdk:11-jdk AS INTERMEDIATE_STAGE
COPY --from=BUILD_IMAGE /vprofile-project/container.sh /container.sh

# Final stage
FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Sabari"
RUN rm -rf /usr/local/tomcat/webapps/*

# Copy container.sh from intermediate stage
COPY --from=INTERMEDIATE_STAGE /container.sh /usr/local/bin/container.sh
RUN chmod +x /usr/local/bin/container.sh

# Copy WAR file from the build stage
COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["container.sh", "run"]

