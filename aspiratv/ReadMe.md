** AspiraTV ** 
Docker for AspiraTV
(Windows / Mac / Linux) lastest release from https://github.com/simulot/aspiratv

Ce programme interroge les serveurs de télévision de rattrapage et télécharge les émissions souhaitées et les enregistre sur un disque 
selon une organisation reconnue par des programmes comme PLEX ou EMBY. Les métadonnées (titre des émissions, desciption, vignettes) 
sont placées de façon à être directement reconnues par Emby (à tester dans Plex).

How to run :
docker run -v c:\\temp\\aspiratv\\data:/var/www/aspiratv/data -v c:\\tem\\aspiratv\\config.json:/var/www/aspiratv/config.json nonobis/aspiratv

You can extract manga from volume if you want.