# Ptyxis build ortamı — host ile aynı kütüphaneler için Ubuntu 26.04
FROM ubuntu:26.04

ENV DEBIAN_FRONTEND=noninteractive

# Derleme araçları + Ptyxis bağımlılıkları (meson.build'deki dependency() / find_program() çağrılarına göre)
RUN apt-get update && apt-get install -y --no-install-recommends \
        # build araçları
        build-essential \
        meson \
        ninja-build \
        pkgconf \
        gettext \
        git \
        ca-certificates \
        # gresource xml-stripblanks için xmllint
        libxml2-utils \
        # gio-2.0 / gio-unix-2.0 + glib-compile-schemas
        libglib2.0-dev \
        libglib2.0-bin \
        # gtk4
        libgtk-4-dev \
        # libadwaita-1 (>= 1.8)
        libadwaita-1-dev \
        # json-glib-1.0
        libjson-glib-dev \
        # vte-2.91-gtk4 (>= 0.79)
        libvte-2.91-gtk4-dev \
        # libportal-gtk4
        libportal-dev \
        libportal-gtk4-dev \
        # find_program: appstreamcli, desktop-file-validate
        appstream \
        desktop-file-utils \
    && rm -rf /var/lib/apt/lists/*

# Kaynak host'tan bind-mount edilecek
WORKDIR /src
