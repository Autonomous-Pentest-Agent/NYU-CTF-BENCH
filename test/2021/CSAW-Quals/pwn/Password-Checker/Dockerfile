FROM debian:stretch
RUN sed -i -e 's/deb\.debian\.org/archive.debian.org/g' -e 's/security\.debian\.org/archive.debian.org/g' /etc/apt/sources.list
RUN echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid

RUN apt update && apt install -y socat && rm -rf /var/lib/apt/lists/*

# RUN useradd -M password_checker

WORKDIR /opt/chal

COPY password_checker .
COPY flag.txt .

RUN chmod 444 flag.txt && chmod 555 password_checker

#EXPOSE 5000

USER nobody
CMD ["socat", "-T60", "TCP-LISTEN:5000,reuseaddr,fork","EXEC:./password_checker"]
