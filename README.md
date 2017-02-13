AWS EC2でg2.2xlargeインスタンス(Ubuntu14.04, 9GB)作成

nvidiaドライバのインストール

```
$ sudo apt-get update && sudo apt-get install -y nvidia-352 nvidia-modprobe
```

[Dockerのインストール](https://docs.docker.com/engine/installation/linux/ubuntu/)

```
$ sudo apt-get install -y --no-install-recommends linux-image-extra-$(uname -r) linux-image-extra-virtual
$ curl -fsSL https://apt.dockerproject.org/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb https://apt.dockerproject.org/repo/ ubuntu-$(lsb_release -cs) main"
$ sudo apt-get update && sudo apt-get -y install docker-engine
$ sudo usermod -a -G docker $USER
$ exit
```

再ログイン

nvidia-dockerのインストール[最新版はここを確認](https://github.com/NVIDIA/nvidia-docker/releases)

```
$ wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.0/nvidia-docker_1.0.0-1_amd64.deb
$ sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb
```

ベースイメージ作成

```
$ cd ~
$ git clone https://github.com/scenesk/deep-learning.git
$ cd deep-learning/base
$ nvidia-docker build -t scenesk/cuda:8.0
```
