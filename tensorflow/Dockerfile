FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04
MAINTAINER ScenesK

RUN apt-get update && apt-get install -y \
    python3-dev \
    python3-pip \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN echo "alias python=python3" >> ~/.bashrc

# TensorFlow 0.12.1
RUN pip3 install --upgrade pip \
 && pip3 install --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-0.12.1-cp35-cp35m-linux_x86_64.whl

WORKDIR /root
