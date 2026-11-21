FROM python:3.6.6-stretch
RUN sed -i -e 's/deb\.debian\.org/archive.debian.org/g' -e 's/security\.debian\.org/archive.debian.org/g' /etc/apt/sources.list
RUN echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid
MAINTAINER Sai Vegasena

#installation
RUN apt-get update && apt-get install -y \
    apt-utils \
    build-essential \
    socat

#user
WORKDIR /app
ADD . /app
RUN chmod -R 700 /app

EXPOSE 4324

ENTRYPOINT ["socat","-T20" ,"TCP-LISTEN:4324,reuseaddr,fork","EXEC:/app/run.sh"]
