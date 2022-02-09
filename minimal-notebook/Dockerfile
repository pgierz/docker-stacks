# Copyright (c) Jupyter Development Team.
# Distributed under the terms of the Modified BSD License.
ARG OWNER=pgierz
ARG BASE_CONTAINER=$OWNER/base-notebook
FROM $BASE_CONTAINER:centos7

LABEL maintainer="Jupyter Project <jupyter@googlegroups.com>"

USER root



# Install all OS dependencies for fully functional notebook server
RUN yum -y upgrade
RUN yum -y install \
    # Common useful utilities
    git \
    tzdata \
    unzip \
    vim-minimal \
    # git-over-ssh
    openssh-clients \
    # TODO: check if these are needed and describe
    inkscape \
    libSM \
    libXext-devel \
    libXrender \
    libXfont \
    xorg-x11-fonts-100dpi \
    nc \
    # nbconvert dependencies
    # https://nbconvert.readthedocs.io/en/latest/install.html#installing-tex
    texlive-xetex \
    texlive-collection-fontsrecommended \
    texlive-plain
RUN yum -y clean all

# Create alternative for nano -> nano-tiny
RUN update-alternatives --install /usr/bin/nano nano /bin/nano-tiny 10

# Switch back to jovyan to avoid accidental container runs as root
USER ${NB_UID}
