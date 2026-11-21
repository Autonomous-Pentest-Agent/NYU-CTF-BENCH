FROM rust:slim-buster
RUN sed -i -e 's/deb\.debian\.org/archive.debian.org/g' -e 's/security\.debian\.org/archive.debian.org/g' /etc/apt/sources.list
RUN echo 'Acquire::Check-Valid-Until "false";' > /etc/apt/apt.conf.d/99no-check-valid

WORKDIR /app

COPY Cargo.toml Cargo.lock /app/
COPY src/lib.rs src/main.rs /app/src/
COPY static /app/static
COPY templates /app/templates

RUN apt-get -y update \
  && apt-get -y install build-essential m4 \
  && cargo build --release \
  && cp /app/target/release/iBad /app/ \
  && rm -rf target

USER nobody
CMD /app/iBad
