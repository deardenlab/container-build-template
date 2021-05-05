FROM ubuntu:20.04

LABEL SOFTWARE_NAME masurca 4.0.3
LABEL MAINTAINER "Tom Harrop"
LABEL VERSION "masurca 4.0.3"

ENV DEBIAN_FRONTEND=noninteractive
ENV LC_ALL=C

RUN     apt-get clean && \
		rm -r /var/lib/apt/lists/* && \
		apt-get update && apt-get upgrade -y --fix-missing

RUN		apt-get install -y \
        build-essential \
        curl \
        git \
        libboost-dev \
        libbz2-dev \
        wget \
        zlib1g-dev

RUN     mkdir /masurca && \
    	wget -O "/masurca.tar.gz" \
	        --no-check-certificate \
	        https://github.com/alekseyzimin/masurca/releases/download/v4.0.3/MaSuRCA-4.0.3.tar.gz &&\
	    tar -zxf /masurca.tar.gz \
    	    -C /masurca \
        	--strip-components 1

WORKDIR /masurca

RUN	    DEST=/usr/local ./install.sh

WORKDIR /

RUN	    rm -r /masurca.tar.gz /masurca

ENTRYPOINT ["/usr/local/bin/masurca"]