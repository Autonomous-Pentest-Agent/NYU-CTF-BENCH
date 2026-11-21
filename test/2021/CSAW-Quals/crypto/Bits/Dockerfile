FROM rust:slim-buster as builder
RUN sed -i -e 's/deb\.debian\.org/archive.debian.org/g' -e 's/security\.debian\.org/archive.debian.org/g' /etc/apt/sources.list
RUN echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid
WORKDIR /app
COPY Cargo.toml Cargo.lock /app/
COPY src/lib.rs src/main.rs /app/src/
RUN apt-get -y update && apt-get -y install build-essential m4 && cargo build --release

FROM debian:buster-slim

RUN apt-get -y update && apt-get -y install socat
WORKDIR /app
COPY --from=builder /app/target/release/hardcore /app/
USER nobody

CMD ["socat", "-T60", "TCP-LISTEN:5000,reuseaddr,pktinfo,fork,ignoreeof", "EXEC:/app/hardcore"]
