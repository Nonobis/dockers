# dockers
All my dockers

** Remotely **

Docker for installing lastest release of "Remotely" from https://github.com/lucent-sea/Remotely.

- A remote control and remote scripting solution, built with .NET Core, SignalR Core, and WebRTC.

Image removed on docker, i am now using unraid package done by Marzel's

** Diacamma **
Docker for installing diacamma release from https://github.com/Diacamma2/syndic

** TachiDesk ** 
Docker for TachiDesk, a port of Tachyiomi on Desktop (Windows / Mac / Linux) lastest release from https://github.com/AriaMoradi/Tachidesk

How to run :
docker run -p 4567:4567 -v your_folder:/root/.local/share/Tachidesk/manga -e TZ='Europe/Paris' -e 'PGID'='100' -e 'PUID'='99' --restart unless-stopped nonobis/tachidesk

You can extract manga from volume if you want.
