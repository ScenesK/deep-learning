FROM nvidia/cuda:8.0-runtime-ubuntu14.04
MAINTAINER ScenesK

RUN echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1404/x86_64 /" > /etc/apt/sources.list.d/nvidia-ml.list
ENV CUDNN_VERSION 5
RUN apt-get update && apt-get install -y --no-install-recommends \
    libcudnn5=5.1.10-1+cuda8.0 \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

 RUN apt-get update && apt-get install -y \
     python3-dev \
     python3-pip \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*
