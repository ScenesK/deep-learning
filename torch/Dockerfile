FROM nvidia/cuda:8.0-cudnn5-devel-ubuntu16.04
MAINTAINER ScenesK

RUN apt-get update && apt-get install -y \
    python3-dev \
    python3-pip \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN echo "alias python=python3" >> ~/.bashrc

# PyTorch 0.1.8
RUN pip3 install --upgrade pip \
 && pip3 install https://s3.amazonaws.com/pytorch/whl/cu80/torch-0.1.8.post1-cp35-cp35m-linux_x86_64.whl \
    torchvision

WORKDIR /root
