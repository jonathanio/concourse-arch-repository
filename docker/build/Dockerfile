FROM archlinux:base-devel

# Prepare the build user for running makepkg
RUN useradd \
  --create-home --home-dir /build \
  --shell /usr/bin/bash \
  --user-group \
  build
COPY build.sudoers /etc/sudoers.d/build

# Ensure the container is fully up-to-date and cleaned
RUN curl --silent --get \
      --url https://archlinux.org/mirrorlist/ \
      --data "country=GB" --data "use_mirror_status=on" --data "protocol=https" \
    | awk '/#Server/ { printf("Server = %s\n", $3) }' \
    > /etc/pacman.d/mirrorlist \
 && pacman -Syu --noconfirm --noprogressbar \
 && pacman -Scc --noconfirm \
 && rm -rf /var/cache/pacman/pkg/* \
           /usr/share/man/* \
           /tmp/* \
           /var/tmp/*
