FROM maven:3.8.4-openjdk:17 AS BUILD_IMAGE
RUN git clone https://github.com/sabarisathish08/vprofile-project/tree/containers 
WORKDIR /vprofile-project
RUN mvn install -y

FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Sabari"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprrofile-v2.tar /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["container.sh","run"]