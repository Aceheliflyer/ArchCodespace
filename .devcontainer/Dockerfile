FROM archlinux:latest
LABEL maintainer='jarrett.aiken@achl.fr'

RUN \
  pacman-key --init \
  && pacman-key --recv-key FBA220DFC880C036 --keyserver keyserver.ubuntu.com && pacman-key --lsign-key FBA220DFC880C036 \
  && pacman -U --noconfirm 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst' \
  && echo -e '\n[chaotic-aur]' >> /etc/pacman.conf && echo 'Include = /etc/pacman.d/chaotic-mirrorlist' >> /etc/pacman.conf \
  && pacman -Syu --noconfirm && pacman -Fy

RUN \
  pacman -S --noconfirm \
  fish \
  git-lfs \
  github-cli \
  git \
  paru \
  sudo

RUN \
  useradd -m codespace -p $(openssl passwd -5 "password") \
  && usermod -aG wheel codespace \
  && sed -i '85 s/# //' /etc/sudoers
USER codespace
WORKDIR /home/codespace

COPY . .
RUN ./setup.sh
