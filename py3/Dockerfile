# Distribution name
FROM nvidia/cuda:10.2-cudnn7-devel

MAINTAINER Queyrel Maxence <maxencequeyrel@hotmail.com>

ENV DEBIAN_FRONTEND="noninteractive"

# Install dependencies
RUN apt-get update -y && \
	apt-get install bzip2 -y && \
	apt-get install wget -y && \
	wget https://repo.anaconda.com/archive/Anaconda3-2020.02-Linux-x86_64.sh && \
	chmod 755 Anaconda3-2020.02-Linux-x86_64.sh && \
	bash Anaconda3-2020.02-Linux-x86_64.sh -b -p /anaconda && \
	rm Anaconda3-2020.02-Linux-x86_64.sh

# Change PATH for anaconda
ENV PATH=$PATH:/anaconda/bin/

# Install Tensorflow
RUN pip install tensorflow

# Install pytorch
RUN conda install pytorch torchvision torchtext cudatoolkit=10.2 -c pytorch

# Install torchmeta
RUN pip install torchmeta

# Install ray and ax
RUN pip install ax-platform
RUN pip install 'ray[tune]'

# Add a notebook profile.
RUN mkdir -p -m 700 /root/.jupyter/ && \
    echo "c.NotebookApp.ip = '*'" >> /root/.jupyter/jupyter_notebook_config.py && \
    rm -rf /var/lib/apt/lists/*

CMD jupyter notebook --ip 0.0.0.0 --no-browser --allow-root

