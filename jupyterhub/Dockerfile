FROM tensorflow/tensorflow:latest-gpu-py3
ARG JUPYTERHUB_VERSION=0.8.1
RUN pip3 install --no-cache \
    jupyterhub==$JUPYTERHUB_VERSION

RUN useradd -m jupyter-user \
    && usermod -aG sudo jupyter-user
ENV HOME=/home/jupyter-user
WORKDIR $HOME
USER jupyter-user

CMD ["jupyterhub-singleuser"]

