FROM ubuntu:latest
MAINTAINER Arnaud Dartois <nonobis@gmail.com>

######################################################################################################################
########################################### Environnement Variables ##################################################
# Set for all apt-get install, must be at the very beginning of the Dockerfile.	
ENV DEBIAN_FRONTEND=noninteractive 
ENV REPO_URL=https://api.github.com/repos/AriaMoradi/Tachidesk/releases/latest

######################################################################################################################
########################################### Expose Port or Volumes ###################################################
EXPOSE 4567
VOLUME [ "/data" ]

######################################################################################################################
################################################# Install prerequisites ##############################################
RUN apt-get update && apt-get install -y \
	curl git \
	openjdk-8-jdk \
	acl
RUN apt-get update

######################################################################################################################
####################################### Download lastest JAR #########################################################
RUN mkdir -p /var/www/tachidesk
RUN  curl -L $(curl -s ${REPO_URL} | grep -o "https.*jar") -o /var/www/tachidesk/latest.jar
RUN setfacl -R -m u:www-data:rwx /var/www/tachidesk/
RUN chown -R www-data:www-data /var/www/tachidesk/

######################################################################################################################
####################################### START Application ############################################################
WORKDIR /var/www/tachidesk
CMD ["java","-jar","/var/www/tachidesk/latest.jar"]
RUN ./scripts/build.sh