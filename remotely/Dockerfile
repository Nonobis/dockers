FROM ubuntu:18.04
MAINTAINER Arnaud Dartois <nonobis@gmail.com>

######################################################################################################################
########################################### Environnement Variables ##################################################
# Set for all apt-get install, must be at the very beginning of the Dockerfile.	
ENV DEBIAN_FRONTEND=noninteractive 
ENV ASPNETCORE_ENVIRONMENT="Production"
ENV ASPNETCORE_URLS http://*:5000

######################################################################################################################
########################################### Expose Port or Volumes ###################################################
EXPOSE 5000/tcp

######################################################################################################################
################################################# Install prerequisites ##############################################
RUN apt-get update 
RUN apt-get upgrade -y
RUN apt-get -y install wget unzip acl ffmpeg libc6-dev libgdiplus
RUN apt-get update	
RUN apt-get -y install software-properties-common

######################################################################################################################
################################################# Install Net Core ###################################################

# Install the .NET Core Repository
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
RUN dpkg -i packages-microsoft-prod.deb

# Install net-core dependency
RUN apt-get update	
RUN add-apt-repository universe
RUN apt-get -y install apt-transport-https

# Install the .NET Core SDK
RUN apt-get update	
RUN apt-get -y  install dotnet-sdk-3.1

######################################################################################################################
################################ Download and Install Application ####################################################
ENV RELEASE_VERSION $(curl -s https://api.github.com/repos/lucent-sea/Remotely/releases/latest | grep "browser_download_url" | grep "Linux-x64" | cut -d'v' -f2 | cut -d'"' -f1)
RUN echo 'Last version to download : ${RELEASE_VERSION}'

RUN mkdir -p /var/www/remotely/
RUN wget "https://github.com/lucent-sea/Remotely/releases/download/v${RELEASE_VERSION}/Remotely_Server_Linux-x64.zip"
RUN unzip -o Remotely_Server_Linux-x64.zip -d /var/www/remotely/
RUN rm Remotely_Server_Linux-x64.zip
RUN setfacl -R -m u:www-data:rwx /var/www/remotely/
RUN chown -R www-data:www-data /var/www/remotely/

WORKDIR /var/www/remotely/
VOLUME /var/www/remotely
ENTRYPOINT ["dotnet", "Remotely_Server.dll"]
