# docker deep learning

### Packages and libraries deployed in the image
- cuda
- cudnn
- Anaconda python 3.8
- TensorFlow / Keras
- pyTorch
- torchtext
- torchvision
- torchaudio
- ray[tune]
- ax

### Package Mandatory
nvidia-docker is mandatory because all the libraries are installed with GPU enable. See the documentation on the github page : https://github.com/NVIDIA/nvidia-docker

#### Download the image
docker pull maxence27/deep_learning:tag (e.g. tag=cuda113-cudnn8)

#### Run the image
docker run -it --gpus=all maxence27/deep_learning:cuda113-cudnn8 bash

If you want to use jupyter notebook run : </br>
docker run -it -p 80:80 --gpus=all maxence27/deep_learning:cuda113-cudnn8 jupyter notebook --ip 0.0.0.0 --port=80 --no-browser --allow-root




