FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu14.04
MAINTAINER ScenesK

RUN apt-get update && apt-get install -y \
    python3-dev \
    python3-pip \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN echo "alias python=python3" >> ~/.bashrc

# Chainer 1.20.0.1
RUN pip3 install --upgrade pip \
 && pip3 install chainer==1.20.0.1

WORKDIR /root
