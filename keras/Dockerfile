FROM scenesk/cuda:8.0
MAINTAINER ScenesK

RUN apt-get update && apt-get install -y \
    gfortran \
    liblapack-dev \
    libblas-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*
RUN pip3 install --upgrade pip

# TensorFlow 0.12.1
RUN export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-0.12.1-cp34-cp34m-linux_x86_64.whl \
 && pip3 install --upgrade $TF_BINARY_URL

# Keras 1.2.2
RUN pip3 install keras==1.2.2
