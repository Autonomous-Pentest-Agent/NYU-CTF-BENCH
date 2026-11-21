FROM debian:stretch
RUN sed -i -e 's/deb\.debian\.org/archive.debian.org/g' -e 's/security\.debian\.org/archive.debian.org/g' /etc/apt/sources.list
RUN echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid

        RUN apt-get update && apt-get upgrade -y && dpkg --add-architecture i386 && apt-get update && apt-get install -y libc6-i386 socat file && rm -rf /var/lib/apt/lists/*

        RUN useradd -M chal

        WORKDIR /opt/chal

        COPY binary_17 .
        COPY message.txt .
        COPY binary_17.txt .

        RUN chown -R root:chal /opt/chal &&           chmod 444 /opt/chal/message.txt &&           chmod 555 /opt/chal/binary_17 &&           chmod 444 /opt/chal/binary_17.txt

        EXPOSE 5000
        USER chal
        CMD ["socat", "-T60", "TCP-LISTEN:5000,reuseaddr,fork", "EXEC:./binary_17"]
        