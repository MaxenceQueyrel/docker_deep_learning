# Distribution name
FROM nvidia/cuda:11.4.0-cudnn8-devel-ubuntu20.04

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

# Install tensorflow, pytorch, pytorch lightning, torchvision, torchaudio, torchtext, ax and ray tune
RUN pip install tensorflow==2.9.1 && \
  pip3 install torch==1.11.0 torchvision==0.12.0 torchaudio==0.11.0 --extra-index-url https://download.pytorch.org/whl/cu113 && \
  pip install torchtext==0.12.0 && \
  pip install ax-platform==0.2.5.1 && \
  pip install 'ray[tune]' && \
  pip install pytorch-lightning==1.6.4


