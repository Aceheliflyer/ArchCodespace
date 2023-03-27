FROM archlinux:latest
LABEL maintainer="jarrett.aiken@achl.fr"

RUN \
  useradd -m codespace

USER codespace
WORKDIR /home/codespace

COPY . .
RUN ./setup.sh
