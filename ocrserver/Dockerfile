FROM golang:1.12
MAINTAINER Arnaud Dartois <nonobis@gmail.com>

ENV GO111MODULE=on

RUN apt-get -qq update \
  && apt-get install -y \
    libleptonica-dev \
    libtesseract-dev \
	imagemagick \
	tesseract-ocr

# Install the training tools by running, within the Tesseract directory:
# RUN make \
# make training \
# make training-install

# Load languages
RUN apt-get install -y \
  tesseract-ocr-all

ADD . $GOPATH/src/github.com/otiai10/ocrserver
WORKDIR $GOPATH/src/github.com/otiai10/ocrserver
RUN go get ./...
RUN go test -v github.com/otiai10/gosseract

ARG LOAD_LANG=all
RUN if [ -n "${LOAD_LANG}" ]; then apt-get install -y tesseract-ocr-${LOAD_LANG}; fi

ENV PORT=8080
CMD $GOPATH/bin/ocrserver
