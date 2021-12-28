# Distribution name
FROM nvidia/cuda:11.3.0-cudnn8-devel

LABEL org.opencontainers.image.authors="maxxxqueyrel@gmail.com"

ARG DEBIAN_FRONTEND="noninteractive"

# Install dependencies
RUN apt-get update -y && \
	apt-get install bzip2 -y && \
	apt-get install wget -y

ARG miniconda_version=Miniconda3-py38_4.10.3-Linux-x86_64.sh
RUN wget https://repo.anaconda.com/miniconda/$miniconda_version && \
	chmod 755 $miniconda_version && \
	bash $miniconda_version -b -p /anaconda && \
	rm $miniconda_version

# Change PATH for anaconda
ENV PATH=$PATH:/anaconda/bin/

# Install tensorflow, pytorch, torchvision, torchaudio, torchtext, ax and ray
RUN pip install tensorflow && \
  pip3 install torch==1.10.1+cu113 torchvision==0.11.2+cu113 torchaudio==0.10.1+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html && \
  pip install torchtext && \
  pip install ax-platform && \
  pip install 'ray[tune]' && \
  pip install pytorch-lightning


