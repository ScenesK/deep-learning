## 環境構築

### NVIDIAドライバ

AWS EC2でg2.2xlargeインスタンス(Ubuntu16.04)作成

依存ライブラリのインストール

```
$ sudo apt update && sudo apt -y install build-essential linux-image-extra-virtual
```

```
sudo vi /etc/modprobe.d/blacklist-nouveau.conf
```

以下の内容でファイル作成

> blacklist nouveau
> options nouveau modeset=0

再起動

```
$ sudo update-initramfs -u
$ sudo reboot
```

接続が切れるので再ログイン

```
$ sudo apt -y install linux-headers-$(uname -r)
```

nvidiaドライバのインストール([最新版はここを確認](http://www.nvidia.com/Download/index.aspx?lang=jp):GRID/GRID Series/GRID K520/Linux 64-bit/Japanese)

```
$ wget -O ~/NVIDIA-Linux-x86_64.run http://jp.download.nvidia.com/XFree86/Linux-x86_64/367.57/NVIDIA-Linux-x86_64-367.57.run
$ sudo sh ~/NVIDIA-Linux-x86_64.run -a --disable-nouveau && rm ~/NVIDIA-Linux-x86_64.run
```

### [Docker](https://docs.docker.com/engine/installation/linux/ubuntu/)

```
$ curl -fsSL https://apt.dockerproject.org/gpg | sudo apt-key add -
$ sudo add-apt-repository "deb https://apt.dockerproject.org/repo/ ubuntu-$(lsb_release -cs) main"
$ sudo apt update && sudo apt -y install docker-engine
```

sudoをつけずに実行できるように設定

```
$ sudo usermod -a -G docker $USER
$ exit
```

再ログイン

### NVIDIA Docker([最新版はここを確認](https://github.com/NVIDIA/nvidia-docker/releases))

```
$ wget -P /tmp https://github.com/NVIDIA/nvidia-docker/releases/download/v1.0.0/nvidia-docker_1.0.0-1_amd64.deb
$ sudo dpkg -i /tmp/nvidia-docker*.deb && rm /tmp/nvidia-docker*.deb
```

### コンテンツのダウンロード

```
$ cd ~
$ git clone https://github.com/scenesk/deep-learning.git
```

## 各ライブラリ用のDockerイメージ作成

全てのイメージを作成すると24GB以上のストレージが必要なので、使うものだけ構築

```
$ cd ~/deep-learning
$ nvidia-docker build -t scenesk/dlstf:0.1 ./tensorflow/
$ nvidia-docker build -t scenesk/dlskeras:0.1 ./keras/
$ nvidia-docker build -t scenesk/dlschainer:0.1 ./chainer/
$ nvidia-docker build -t scenesk/dlsmx:0.1 ./mxnet/
$ nvidia-docker build -t scenesk/dlscntk:0.1 ./cntk/
$ nvidia-docker build -t scenesk/dlstorch:0.1 ./torch/
```
