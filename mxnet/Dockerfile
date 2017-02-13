FROM scenesk/cuda:8.0
MAINTAINER ScenesK

RUN apt-get update && apt-get install -y \
    git \
    libopenblas-dev \
    libopencv-dev \
 && apt-get clean \
 && rm -rf /var/lib/apt/lists/*

RUN pip3 install --upgrade pip && pip3 install \
    graphviz==0.5.2 \
    numpy==1.12.0

RUN git clone --recursive https://github.com/dmlc/mxnet ~/mxnet \
 && cd ~/mxnet \
 && cp make/config.mk . \
 && echo "USE_BLAS=openblas" >> config.mk \
 && echo "USE_CUDA=1" >> config.mk \
 && echo "USE_CUDA_PATH=/usr/local/cuda/" >> config.mk \
 && echo "USE_CUDNN=1" >> config.mk \
 && make -j"$(nproc)" \
 && cd python \
 && python3 setup.py install \
 && rm -rf ~/mxnet
