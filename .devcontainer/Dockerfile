FROM archlinux:latest
LABEL maintainer='jarrett.aiken@achl.fr'

# Add Chaotic AUR support and upgrade system
RUN \
  pacman-key --init \
  && pacman-key --recv-key FBA220DFC880C036 --keyserver keyserver.ubuntu.com && pacman-key --lsign-key FBA220DFC880C036 \
  && pacman -U --noconfirm 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-keyring.pkg.tar.zst' 'https://cdn-mirror.chaotic.cx/chaotic-aur/chaotic-mirrorlist.pkg.tar.zst' \
  && echo -e '\n[chaotic-aur]\nInclude = /etc/pacman.d/chaotic-mirrorlist' >> /etc/pacman.conf \
  && pacman -Syu --noconfirm && pacman -Fy

# Install packages
RUN \
  pacman -S --noconfirm \
  fish \
  git-lfs \
  github-cli \
  git \
  paru \
  sudo

# Setup user and sudo permissions
RUN \
  useradd -m codespace -p $(openssl passwd -5 "password") \
  && chsh -s /usr/bin/fish codespace \
  && usermod -aG wheel codespace \
  && sed -i '85 s/^# //' /etc/sudoers

USER codespace
WORKDIR /home/codespace
