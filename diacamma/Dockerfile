FROM debian:stretch
MAINTAINER Arnaud Dartois <nonobis@gmail.com>

######################################################################################################################
########################################### Environnement Variables ##################################################
# Set for all apt-get install, must be at the very beginning of the Dockerfile.	
ENV DEBIAN_FRONTEND=noninteractive 

######################################################################################################################
################################################# Install prerequisites ##############################################
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get install -y default-libmysqlclient-dev
RUN apt-get install -y locales 
RUN apt-get install -y locales-all sudo
RUN rm -rf /var/lib/apt/lists/*
RUN locale-gen fr_FR.UTF-8
	
######################################################################################################################
################################ INSTALL PYHTON      #################################################################
RUN apt-get install libssl-dev openssl
RUN wget https://www.python.org/ftp/python/3.5.0/Python-3.5.0.tgz
RUN tar xzvf Python-3.5.0.tgz
RUN cd Python-3.5.0
RUN ./configure --prefix /usr/local
RUN make
RUN make install

######################################################################################################################
########################################### Environnement Variables ##################################################
ENV LANG fr_FR.UTF-8
ENV LANGUAGE fr_FR:fr
ENV LC_ALL fr_FR.UTF-8
ENV ASSO_VERSION_CONSTRAINT=""
ENV SYNDIC_VERSION_CONSTRAINT=""
ENV LUCTERIOS_VERSION_CONSTRAINT=""

######################################################################################################################
################################ Download and Install Application ####################################################
RUN curl --location -o /tmp/Diacamma_setup.tar.gz http://www.sd-libre.fr/download/Diacamma_setup.tar.gz && \
    cd /tmp && \
    tar zxvf /tmp/Diacamma_setup.tar.gz && \
    apt-get update && \
    /tmp/Diacamma/install.sh -p "diacamma-asso${ASSO_VERSION_CONSTRAINT} diacamma-syndic${SYNDIC_VERSION_CONSTRAINT} lucterios-standard${LUCTERIOS_VERSION_CONSTRAINT}" && \
    rm -rf /var/lib/apt/lists/*

RUN cd /var/lucterios2
RUN . virtual_for_lucterios/bin/activate
RUN pip install gunicorn psycopg2-binary mysqlclient

COPY entrypoint.d/ /entrypoint.d/
COPY bin/backup.sh /usr/local/bin/backup
COPY bin/restore.sh /usr/local/bin/restore
COPY bin/version.sh /usr/local/bin/version

RUN chmod +x /entrypoint.d/entrypoint.sh
RUN /usr/local/bin/backup
RUN /usr/local/bin/restore
RUN /usr/local/bin/version

VOLUME [ "/backups" ]

ENTRYPOINT [ "/entrypoint.d/entrypoint.sh" ]
CMD [ "run" ]
