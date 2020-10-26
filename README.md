# dockers
All my dockers

** Remotely **

Docker for installing lastest release of "Remotely" from https://github.com/lucent-sea/Remotely.

- A remote control and remote scripting solution, built with .NET Core, SignalR Core, and WebRTC.

How to run :

docker run -d --name='remotely' --net='bridge' -e TZ="Europe/Paris" -e HOST_OS="Unraid" -e 'ConnectionStrings__SQLite'='DataSource=Remotely.db' -e 'ConnectionStrings__SQLServer'='Server=(localdb)\\mssqllocaldb;Database=Remotely-Server-53bc9b9d-9d6a-45d4-8429-2a2761773502;Trusted_Connection=True;MultipleActiveResultSets=true' -e 'ConnectionStrings__PostgreSQL'='Host=192.168.1.18;Database=remotely;Username=postgres;Password=p@ssw0rd!' -e 'ApplicationOptions__DBProvider'='PostgreSQL' -e 'ApplicationOptions__SmtpHost'='smtp.gmail.com' -e 'ApplicationOptions__SmtpPort'='587' -e 'ApplicationOptions__SmtpUserName'='nonobis@gmail.com' -e 'ApplicationOptions__SmtpPassword'='vbypnmqnoownkxlv' -e 'ApplicationOptions__SmtpEmail'='noreply@tordais.one' -e 'ApplicationOptions__SmtpDisplayName'='Remotely Administrator' -e 'ApplicationOptions__SmtpEnableSsl'='true' -e 'ApplicationOptions__UseWebRtc'='true' -e 'ApplicationOptions__UseHsts'='false' -e 'ApplicationOptions_DataRetentionInDays'='90' -e 'ApplicationOptions_DefaultPrompt'='~>' -e 'ApplicationOptions_EnableWindowsEventLog'='true' -p '8199:5000/tcp' 'nonobis/remotely:latest'