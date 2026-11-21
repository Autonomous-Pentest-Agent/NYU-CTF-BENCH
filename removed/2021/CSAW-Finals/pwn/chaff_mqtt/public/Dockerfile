FROM debian:stretch
RUN sed -i -e 's/deb\.debian\.org/archive.debian.org/g' -e 's/security\.debian\.org/archive.debian.org/g' /etc/apt/sources.list
RUN echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid
RUN apt-get update
RUN apt-get install -y g++-multilib socat

RUN mkdir /opt/chal
WORKDIR /opt/chal
COPY ./mqtt_strip ./
RUN sh -c 'echo flag{test_flag_goes_here} > flag'
RUN chmod 444 flag && chmod 555 mqtt_strip

USER nobody
CMD ["socat", "-T30", "TCP-LISTEN:5000,reuseaddr,fork","EXEC:./mqtt_strip"]
