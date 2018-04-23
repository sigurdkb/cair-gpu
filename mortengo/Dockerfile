FROM nvidia/cuda:9.1-cudnn7-devel

RUN apt-get update && apt-get install -y \
    nano \
    joe \
    vim \
    emacs \
    openssh-client \
    python-pip \
    && rm -rf /var/lib/apt/lists/*

RUN pip install keras hdf5storage h5py numpy Cython sklearn
