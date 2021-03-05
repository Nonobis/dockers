FROM golang:alpine as builder
MAINTAINER Arnaud Dartois <nonobis@gmail.com>

######################################################################################################################
########################################### Building aspiraTV  #######################################################
WORKDIR /go/src/aspiratv
RUN apk add git
RUN git clone https://github.com/simulot/aspiratv.git .
RUN go install -v ./...

######################################################################################################################
########################################### Environnement Variables ##################################################
# Set for all apt-get install, must be at the very beginning of the Dockerfile.	
ENV DEBIAN_FRONTEND=noninteractive 
ENV MAX_CONCURRENT_DOWNLOAD=12
ENV LOG_LEVEL=ERROR 

######################################################################################################################
################################################# Install prerequisites ##############################################
FROM alpine
COPY --from=builder /go/bin/aspiratv .
RUN apk add --no-cache ffmpeg

######################################################################################################################
################################################# Expose Volume ######################################################
RUN mkdir -p /var/www/aspiratv/config
RUN mkdir -p /var/www/aspiratv/data
VOLUME [ "/var/www/aspiratv/data", "/var/www/aspiratv/config.json", "/var/www/aspiratv/aspiratv.log" ]

################################################# Run Application  ###################################################
CMD ["./aspiratv", "run --config config.json --headless --log aspiratv.log --log-level $(LOG_LEVEL) --max-tasks $(MAX_CONCURRENT_DOWNLOAD"]

