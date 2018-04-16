FROM tensorflow/tensorflow:latest-devel-gpu-py3

RUN apt-get update && apt-get install -y \
    nano \
    joe \
    vim \
    protobuf-compiler \
    python3-tk \
    build-essential \
    cmake \
    git \
    yasm \
    pkg-config \
    libswscale-dev \
    libtbb2 \
    libtbb-dev \
    libjpeg-dev \
    libpng-dev \
    libtiff-dev \
    libjasper-dev \
    libavformat-dev \
    libavcodec-dev \
    libpq-dev \
    libgtk2.0-dev \
    libdc1394-22-dev \
    libv4l-dev \
    libwebp-dev \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install \
    keras \
    hdf5storage \
    h5py \
    pillow \
    lxml \
    jupyter \
    matplotlib \
    numpy \
    pandas

WORKDIR /root/

RUN git clone https://github.com/tensorflow/models.git \
    && cd models/research \
    && protoc object_detection/protos/*.proto --python_out=.

RUN git clone https://github.com/opencv/opencv.git \
    && mkdir opencv/build \
    && cd opencv/build \
    && cmake .. \
    && make -j20 \
    && make install \
    && rm -rfd /root/opencv/build

ENV PYTHONPATH /root/models/research:/root/models/research/slim

