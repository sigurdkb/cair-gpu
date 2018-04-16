FROM tensorflow/tensorflow:latest-devel-gpu-py3

RUN apt-get update && apt-get install -y \
    nano \
    joe \
    vim \
    emacs \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install keras hdf5storage h5py
