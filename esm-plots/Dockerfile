# Copyright (c) Paul Gierz, AWI Scientific Computing, Bremerhaven, Germany, 2021 
# Distributed under the terms of the Modified BSD License.
ARG OWNER=pgierz
ARG BASE_CONTAINER=$OWNER/datascience-notebook:centos7
FROM $BASE_CONTAINER

LABEL maintainer="Paul Gierz <pgierz@awi.de>"

USER root

RUN yum -y upgrade
RUN yum -y install \
    which \
    less
RUN yum -y clean all

USER ${NB_UID}

ENV NUMBA_CACHE_DIR /tmp
ENV MPLCONFIGDIR /tmp


# PG: Install additional packages for Holoviz 
RUN mamba install --quiet --yes \
  --channel pyviz \
  holoviz
RUN mamba install --quiet --yes \
  --channel conda-forge \
  geoviews
RUN mamba install --quiet --yes \
  --channel conda-forge \
  pyfesom2
RUN mamba install --quiet --yes \
  --channel conda-forge \
  f90nml
RUN mamba install --quiet --yes \
  --channel conda-forge \
  papermill
RUN mamba install --quiet --yes \
  --channel conda-forge \
  cdo python-cdo
RUN mamba install --yes \
  --channel conda-forge \
  numba==0.55.0
RUN mamba install --yes \
  --channel conda-forge \
  gdal
RUN mamba clean --all -f -y && \
  fix-permissions "${CONDA_DIR}" && \
  fix-permissions "/home/${NB_USER}"

COPY pyfesom2/pyfesom2/geojson/ /opt/conda/lib/python3.9/site-packages/pyfesom2/geojson/

RUN python3 -VV && python3 -c "import datashader as ds; print(f'Module datashader version {ds.__version__} loaded from {ds.__file__}')"
RUN python3 -VV && python3 -c "import pyfesom2 as pf2"


WORKDIR "${HOME}"
