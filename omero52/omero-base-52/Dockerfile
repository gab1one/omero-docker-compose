FROM ubuntu:14.04

MAINTAINER hadrien.mary@gmail.com

RUN sed 's/main$/main universe/' -i /etc/apt/sources.list

# Install dependencies
RUN apt-get update && apt-get upgrade -y && apt-get install -y \
    unzip wget supervisor \
    python2.7 python-pil python-matplotlib python-pip \
    python-numpy python-tables python-scipy \
    openjdk-7-jre-headless ice35-services python-zeroc-ice \
    mencoder nano postgresql-client-9.3 postgresql-client-common

ENV BRANCH 5.2.4
ENV LABEL ICE=3.5
ENV ICE 35

# Path variables
ENV OMERO_DIR /omero
ENV OMERO_HOME $OMERO_DIR/OMERO.server

# Add omero user and install omego tools
RUN useradd -m omero
RUN pip install -U omego

RUN mkdir $OMERO_DIR
RUN chown omero $OMERO_DIR

# Download Omero with omego
USER omero
WORKDIR $OMERO_DIR

RUN omego download --branch=$BRANCH --ice $ICE --unzipdir . -v server
RUN rm OMERO.server*zip

RUN ln -s OMERO.server-* $OMERO_HOME

USER root
