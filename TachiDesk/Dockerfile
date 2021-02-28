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
RUN curl -s https://api.github.com/repos/AriaMoradi/Tachidesk/releases/latest | grep "browser_download_url.Tachidesk-v*.jar" | cut -d ":" -f 2,3 | tr -d \" | wget -qi - -o /var/www/tachidesk/latest.jar
RUN setfacl -R -m u:www-data:rwx /var/www/tachidesk/
RUN chown -R www-data:www-data /var/www/tachidesk/

######################################################################################################################
################################################# Create specific user ###############################################
RUN useradd -d /home/tachidesk -ms /bin/bash -g root -G sudo -p ubuntu ubuntu
RUN mkdir /opt/data  && chown ubuntu /opt/data
WORKDIR /home/tachidesk

######################################################################################################################
################################################# Expose Volume ######################################################
VOLUME [ "/opt/data" ]

######################################################################################################################
####################################### START Application ############################################################
WORKDIR /var/www/tachidesk
CMD ["java","-jar","/var/www/tachidesk/latest.jar"]