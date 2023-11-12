## 🧩DL Environment SetUp
### GPU Drive install
File preparation: NVIDIA Drives downloaded from here: https://www.nvidia.cn/Download/index.aspx?lang=cn

Software request: cmake, gcc

* Move and backpack the original open source drivers, since it will not allow other drivers to be installed

``` bash
sudo mv /lib/modules/$(uname -r)/kernel/drivers/gpu/drm/nouveau/nouveau.ko /lib/modules/$(uname -r)/kernel/drivers/gpu/drm/nouveau/nouveau.ko.org
sudo update-initramfs -u
```
* Restart system

* Type the following commands in the fold where you download you driver. We use Driver.run to represent the driver.

``` bash
sudo chmod +x Driver.run
sudo ./Driver.run --no-x-check --no-nouveau-check --no-opengl-files
```
* Select all default options while installing, check the installation with the following commands when finished:

``` bash
nvidia-smi
```

### Cuda Installation
Some computational work needs Compute Unified Device Architecture library(CUDA) such as Tensorflow, Pytorch and Caffe. To install CUDA Runtime ennvironment, please follow these instructions below.

Download CUDA Runtime library from offical source, we recommend to download .run file

https://developer.nvidia.com/cuda-downloads
Then, use sudo sh cuda.run(replace with the file name) to install, notice if you have already installed Nvidia driver, **DO NOT** choose to install driver while installing cuda.

### CUDNN installation
The NVIDIA CUDA Deep Neural Network library (cuDNN) is a GPU-accelerated library of primitives for deep neural networks. We are usually aqucired to install CUDNN for better performance when training. The following instructions will guide you to install CUDNN.

In order to download cuDNN, ensure you are registered for the NVIDIA Developer Program in this [link](https://developer.nvidia.com/cudnn).


Then choose the installation method that meets your environment needs.

Now navigate to directory where the cuDNN Tar file place. Use the following commands.

``` bash
tar -xzvf cudnn-9.0-linux-x64-v7.tgz
sudo cp cuda/include/cudnn.h /usr/local/cuda/include
sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
sudo chmod a+r /usr/local/cuda/include/cudnn.h /usr/local/cuda/lib64/libcudnn*
```

## 👥 Change PIP package source
The official pip source is always stay up to date, however, it may be slow to download packages from this server in some countries, so for some cases, change to Tsinghua server or aliyun server can help to download packges faster.

``` bash
pip install scrapy -i https://pypi.tuna.tsinghua.edu.cn/simple # Tsinghua source
pip install scrapy -i https://mirrors.aliyun.com/pypi/simple/ # or Aliyun source
```

If you want to change the pip source permanently, you can edit ~/.pip/pip.conf and add the following text to this file:

``` bash
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
```

However, mirror souce have some delay to synchronize with the main souce, packages installed in these way may have lower version.