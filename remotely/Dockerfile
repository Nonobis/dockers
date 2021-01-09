FROM ubuntu:18.04
MAINTAINER Arnaud Dartois <nonobis@gmail.com>

######################################################################################################################
########################################### Environnement Variables ##################################################
# Set for all apt-get install, must be at the very beginning of the Dockerfile.	
ENV DEBIAN_FRONTEND=noninteractive 
ENV ASPNETCORE_ENVIRONMENT="Production"
ENV ASPNETCORE_URLS https://*:5000
ENV ASPNETCORE_HTTPS_PORT=5000
ENV ASPNETCORE_Kestrel__Certificates__Default__Path=/var/www/remotely/.aspnet/https/remotely.pfx
ENV ASPNETCORE_Kestrel__Certificates__Default__Password=remotely


######################################################################################################################
########################################### Expose Port or Volumes ###################################################
EXPOSE 5000/tcp

######################################################################################################################
################################################# Install prerequisites ##############################################
RUN apt-get update && apt-get upgrade -y && apt-get -y install wget curl unzip acl ffmpeg libc6-dev libgdiplus software-properties-common

######################################################################################################################
################################################# Install Net Core ###################################################

# Install the .NET Core Repository
RUN wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb && dpkg -i packages-microsoft-prod.deb

# Install net-core dependency
RUN apt-get update && add-apt-repository universe && apt-get -y install apt-transport-https

# Install the .NET Core SDK
RUN apt-get update && apt-get -y install dotnet-sdk-3.1

######################################################################################################################
################################ Download and Install Application ####################################################
RUN mkdir -p /var/www/remotely/
RUN curl -s https://api.github.com/repos/lucent-sea/Remotely/releases/latest | grep "browser_download_url.*Remotely_Server_Linux-x64.zip" | cut -d ":" -f 2,3 | tr -d \" | wget -qi -
RUN unzip -o Remotely_Server_Linux-x64.zip -d /var/www/remotely/
RUN rm Remotely_Server_Linux-x64.zip
RUN setfacl -R -m u:www-data:rwx /var/www/remotely/
RUN chown -R www-data:www-data /var/www/remotely/

# Generate https certificate
RUN mkdir -p /var/www/remotely/.aspnet/https/ 
RUN dotnet dev-certs https --clean && dotnet dev-certs https -ep /var/www/remotely/.aspnet/https/remotely.pfx -p "remotely"

WORKDIR /var/www/remotely/
VOLUME /var/www/remotely
ENTRYPOINT ["dotnet", "Remotely_Server.dll"]
