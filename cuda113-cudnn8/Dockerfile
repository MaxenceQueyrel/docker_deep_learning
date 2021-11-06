# Distribution name
FROM nvidia/cuda:11.3.0-cudnn8-devel

MAINTAINER Queyrel Maxence <maxencequeyrel@hotmail.com>

ENV DEBIAN_FRONTEND="noninteractive"

# Install dependencies
RUN apt-get update -y && \
	apt-get install bzip2 -y && \
	apt-get install wget -y && \
	wget https://repo.anaconda.com/archive/Anaconda3-2021.05-Linux-x86_64.sh && \
	chmod 755 Anaconda3-2021.05-Linux-x86_64.sh && \
	bash Anaconda3-2021.05-Linux-x86_64.sh -b -p /anaconda && \
	rm Anaconda3-2021.05-Linux-x86_64.sh

# Change PATH for anaconda
ENV PATH=$PATH:/anaconda/bin/

# Install tensorflow, pytorch, torchvision, torchaudio, torchtext, ax and ray
RUN pip install tensorflow && \
  pip3 install torch==1.10.0+cu113 torchvision==0.11.1+cu113 torchaudio==0.10.0+cu113 -f https://download.pytorch.org/whl/cu113/torch_stable.html && \
  pip install torchtext && \
  pip install ax-platform && \
  pip install 'ray[tune]'


