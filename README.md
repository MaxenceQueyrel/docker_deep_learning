# docker deep learning

### Packages and libraries deployed in the image
- cuda 10.1 and cudnn 7.0
- Anaconda for python2 or python3 (tag py2 o py3 respectively)
- TensorFlow 2.0.0
- pyTorch 1.3.1
- torchtext 0.4.0
- torchvision 0.4.2
- torchmeta (py3 only) 1.2.1

### Package Mandatory
nvidia-docker is mandatory because all the libraries are installed with GPU enable. See the documentation on the github page : https://github.com/NVIDIA/nvidia-docker

#### Download the image
docker pull maxence27/deep_learning:tag (replace tag by py2 or py3)

#### Run the image
docker run -it --gpus=all maxence27/deep_learning:py2 bash

If you want to use jupyter notebook run : </br>
docker run -it --gpus=all --net=host maxence27/deep_learning:py2


