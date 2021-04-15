FROM ubuntu:latest
MAINTAINER Arnaud Dartois <nonobis@gmail.com>

######################################################################################################################
########################################### Environnement Variables ##################################################
# Set for all apt-get install, must be at the very beginning of the Dockerfile.	
ENV DEBIAN_FRONTEND=noninteractive 

######################################################################################################################
########################################### Expose Port or Volumes ###################################################
EXPOSE 4567

######################################################################################################################
################################################# Install prerequisites ##############################################
RUN apt-get update && apt-get install -y \
	curl wget git \
	openjdk-8-jdk \
	acl
RUN apt-get update

######################################################################################################################
####################################### Download lastest JAR #########################################################
RUN mkdir -p /var/www/tachidesk
RUN mkdir -p /root/.local/share/Tachidesk/extensions
RUN mkdir -p /root/.local/share/Tachidesk/thumbnails
RUN mkdir -p /root/.local/share/Tachidesk/manga
RUN curl -L $(curl -s https://github.com/Suwayomi/Tachidesk/releases/download/v0.3.0-rc2/Tachidesk-v | grep -o "https.*jar") -o /var/www/tachidesk/latest.jar
RUN setfacl -R -m u:www-data:rwx /var/www/tachidesk/
RUN chown -R www-data:www-data /var/www/tachidesk/

######################################################################################################################
################################################# Expose Volume ######################################################
VOLUME [ "/root/.local/share/Tachidesk/extensions", "/root/.local/share/Tachidesk/manga", "/root/.local/share/Tachidesk/thumbnails" ]

######################################################################################################################
####################################### START Application ############################################################
WORKDIR /var/www/tachidesk
CMD ["java","-jar","/var/www/tachidesk/latest.jar","--server.address", "0.0.0.0"]
