# lc0-ubuntu-unofficial-builds

[Lc0](https://github.com/LeelaChessZero/lc0) is an open source neural network based chess engine.

This repository contains several builds of Lc0 for [Ubuntu Linux](https://ubuntu.com/).\
I builded them for personal use, so _this is not an official Lc0 repository_.\
Maybe some will find this useful since [official releases](https://github.com/LeelaChessZero/lc0/releases)
are only for Android and Windows.

The files `lc0-v0.28.2-linux*` & `lc0-v0.29-linux*` were builded on Ubuntu 18.04.\
The files `lc0-v0.30-linux*` were builded on Ubuntu 23.04.

For detailed explanations see https://jldblog.eu/series/lc0/ (in French).

For **Lc0 official releases** (Android & Windows) see https://github.com/LeelaChessZero/lc0/releases.

## How to build Lc0 v0.30 on Ubuntu 23.x (CPU only)

```shell
sudo apt update
sudo apt install git
sudo apt install build-essential
sudo apt install meson
```

```shell
git clone -b release/0.30 --recurse-submodules https://github.com/LeelaChessZero/lc0.git
cd lc0
./build.sh
```

## How to build Lc0 v0.30 on Ubuntu 23.x with Nvidia GPU support

Same process as detailed above for CPU only, but you must also install `nvidia-cuda-toolkit` and `nvidia-cudnn` packages.
To do this first you must enable non-free and contrib repositories, and then install
Nvidia [Cuda](https://developer.nvidia.com/cuda-toolkit) and [cuDNN](https://developer.nvidia.com/cudnn) packages using the commands below:

```shell
sudo apt-add-repository non-free
sudo apt-add-repository contrib
sudo apt update

sudo apt install nvidia-cuda-toolkit
sudo apt install nvidia-cudnn
```

## How to test the build

```shell
cd build/release/
```

Lc0 needs a network to run. The easiest way is to add the one of the official release (`791556.pb.gz`).
It can be found on https://training.lczero.org/networks/. See https://lczero.org/play/networks/bestnets/ for explanations about networks.

```shell
wget https://training.lczero.org/get_network?sha=f404e156ceb2882470fd8c032b8754af0fa0b71168328912eaef14671a256e34 -O 791556.pb.gz
```

And then launch the benchmark with the command :

```shell
./lc0 benchmark
```

You should obtain something like :

```
			   _
		|   _ | |
		|_ |_ |_| v0.30.0 built Aug 28 2023
		Found pb network file: ./791556.pb.gz
		Creating backend [eigen]...
		Using Eigen version 3.4.0
		Eigen max batch size is 256.
        ...
        ...
```

Or if compiled with the Nvidia GPU support :

```
		       _
		|   _ | |
		|_ |_ |_| v0.30.0 built Aug 28 2023
		Found pb network file: ./791556.pb.gz
		Creating backend [cudnn-auto]...
		Switching to [cudnn-fp16]...
		CUDA Runtime version: 11.8.0
		Cudnn version: 8.5.0
		Latest version of CUDA supported by the driver: 12.2.0
		GPU: NVIDIA GeForce GTX 1650 Ti
		GPU memory: 3.81238 GiB
		GPU clock frequency: 1485 MHz
		GPU compute capability: 7.5
        ...
        ...
```

## GUI

dedicated GUI
https://github.com/rooklift/nibbler
