# Distribution name
FROM nvidia/cuda:9.0-cudnn7-devel

MAINTAINER Queyrel Maxence <maxencequeyrel@hotmail.com>

ENV DEBIAN_FRONTEND="noninteractive"

# Install dependencies
RUN apt-get update -y && \
	apt-get install bzip2 -y && \
	apt-get install wget -y && \
	wget https://repo.anaconda.com/archive/Anaconda2-2018.12-Linux-x86_64.sh && \
	chmod 755 Anaconda2-2018.12-Linux-x86_64.sh && \
	bash Anaconda2-2018.12-Linux-x86_64.sh -b -p /anaconda && \
	rm Anaconda2-2018.12-Linux-x86_64.sh

# Change PATH for anaconda
ENV PATH=$PATH:/anaconda/bin/

# Install Tensorflow
RUN pip install --ignore-installed --upgrade tensorflow_gpu

# Install Keras
RUN pip install keras && \
    mkdir /root/.keras

# Install pytorch
RUN conda install pytorch torchvision cudatoolkit=9.0 -c pytorch

# Add a notebook profile.
RUN mkdir -p -m 700 /root/.jupyter/ && \
    echo "c.NotebookApp.ip = '*'" >> /root/.jupyter/jupyter_notebook_config.py && \
    rm -rf /var/lib/apt/lists/*

CMD jupyter notebook --ip 0.0.0.0 --no-browser --allow-root

