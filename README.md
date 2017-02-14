AWS EC2でg2.2xlargeインスタンス(Ubuntu16.04)作成

nvidiaドライバのインストール([最新版はここを確認](https://developer.nvidia.com/cuda-downloads):Linux-x86_64-Ubuntu-16.04-deb(network))

```
$ wget -P /tmp http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.44-1_amd64.deb
$ sudo dpkg -i /tmp/cuda-repo-ubuntu1604_8.0.44-1_amd64.deb && rm /tmp/cuda-repo-ubuntu*.deb
$ sudo apt update && sudo apt -y install cuda
```

[Dockerのインストール](https://docs.docker.com/engine/installation/linux/ubuntu/)

```
$ sudo apt install -y --no-install-recommends linux-image-extra-$(uname -r) linux-image-extra-virtual
$ curl -fsSL https://apt.dockerproject.org/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb https://apt.dockerproject.org/repo/ ubuntu-$(lsb_release -cs) main"
$ sudo apt update && sudo apt -y install docker-engine
$ sudo usermod -a -G docker $USER
$ exit
```

再ログイン

nvidia-dockerのインストール([最新版はここを確認](https://github.com/NVIDIA/nvidia-docker/releases))

```
$ wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.0/nvidia-docker_1.0.0-1_amd64.deb
$ sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb
```

各ライブラリ用の環境構築(全てのイメージを作成すると24GB以上のストレージが必要なので、使うものだけ構築)

```
$ cd ~
$ git clone https://github.com/scenesk/deep-learning.git
$ cd deep-learning
$ nvidia-docker build -t scenesk/dlstf:0.1 ./tensorflow/
$ nvidia-docker build -t scenesk/dlskeras:0.1 ./keras/
$ nvidia-docker build -t scenesk/dlschainer:0.1 ./chainer/
$ nvidia-docker build -t scenesk/dlsmx:0.1 ./mxnet/
$ nvidia-docker build -t scenesk/dlscntk:0.1 ./cntk/
$ nvidia-docker build -t scenesk/dlstorch:0.1 ./torch/
```
