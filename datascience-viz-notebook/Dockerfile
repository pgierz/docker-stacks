# Copyright (c) Paul Gierz, AWI Scientific Computing, Bremerhaven, Germany, 2021 
# Distributed under the terms of the Modified BSD License.
ARG OWNER=jupyter
ARG BASE_CONTAINER=$OWNER/datascience-notebook
FROM $BASE_CONTAINER

LABEL maintainer="Paul Gierz <pgierz@awi.de>"

USER ${NB_UID}

# PG: Install additional packages for Holoviz 
RUN mamba install --quiet --yes \
  --channel pyviz \
  'holoviz' && \
  mamba clean --all -f -y && \
  fix-permissions "${CONDA_DIR}" && \
  fix-permissions "/home/${NB_USER}"


WORKDIR "${HOME}"
