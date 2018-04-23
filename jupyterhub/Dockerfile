FROM tensorflow/tensorflow:latest-gpu-py3
ARG JUPYTERHUB_VERSION=0.8.1

RUN apt-get update && apt-get install -y \
    sudo \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install keras hdf5storage h5py

RUN pip3 install --no-cache \
    jupyterhub==$JUPYTERHUB_VERSION \
    keras \
    hdf5storage \
    h5py

RUN useradd -m jupyter-user \
    && usermod -aG sudo jupyter-user
ENV HOME=/home/jupyter-user
WORKDIR $HOME
USER jupyter-user

CMD ["jupyterhub-singleuser"]

