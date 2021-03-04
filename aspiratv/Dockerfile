FROM ubuntu:latest
MAINTAINER Arnaud Dartois <nonobis@gmail.com>

######################################################################################################################
########################################### Environnement Variables ##################################################
# Set for all apt-get install, must be at the very beginning of the Dockerfile.	
ENV DEBIAN_FRONTEND=noninteractive 
ENV MAX_CONCURRENT_DOWNLOAD=12
ENV LOG_LEVEL=ERROR 

######################################################################################################################
################################################# Install prerequisites ##############################################
RUN apt-get update && apt-get install -y \
	wget git curl unzip acl \
	ffmpeg libc6-dev libgdiplus \
	software-properties-common 
	
######################################################################################################################
####################################### Download lastest release######################################################
RUN mkdir -p /var/www/aspiratv
RUN mkdir -p /var/www/aspiratv/data
RUN mkdir -p /var/www/aspiratv/data/Documentaires
RUN mkdir -p /var/www/aspiratv/data/Jeunesse
RUN mkdir -p /var/www/aspiratv/data/Series
RUN mkdir -p /var/www/aspiratv/data/News
RUN curl -L $(curl -s https://api.github.com/repos/simulot/aspiratv/releases/latest | grep -o "https.*_Linux_x86_64.tar.gz") -o /var/www/aspiratv/latest.tar.gz
RUN cd /var/www/aspiratv/ \
	tar -czvf /var/www/aspiratv/latest.tar.gz
RUN rm /var/www/aspiratv/latest.tar.gz
RUN setfacl -R -m u:www-data:rwx /var/www/aspiratv/
RUN chown -R www-data:www-data /var/www/aspiratv/

######################################################################################################################
################################################# Expose Volume ######################################################
VOLUME [ "/var/www/aspiratv/data", "/var/www/aspiratv/config.json" ]

######################################################################################################################
####################################### START Application ############################################################
WORKDIR /var/www/aspiratv
CMD ["aspiratv", "run", "--config", "/var/www/aspiratv/config.json", "--headless", "--log", "aspiratv.log", "--log-level", "$(LOG_LEVEL)", "--max-tasks", "$(MAX_CONCURRENT_DOWNLOAD)"]