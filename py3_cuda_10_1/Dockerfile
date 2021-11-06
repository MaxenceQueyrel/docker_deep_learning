# Distribution name
FROM nvidia/cuda:10.1-cudnn7-devel

MAINTAINER Queyrel Maxence <maxencequeyrel@hotmail.com>

ENV DEBIAN_FRONTEND="noninteractive"

# Install dependencies
RUN apt-get update -y && \
	apt-get install bzip2 -y && \
	apt-get install wget -y && \
  apt-get update && \
  apt-get install -y build-essential git && \
  apt-get install -y libopenblas-dev liblapack-dev && \
  apt-get install -y libopencv-dev && \
  apt-get install -y graphviz && \
  apt-get install -y libssl-dev && \
  apt-get install -y gfortran

# Install Anaconda
RUN	wget https://repo.anaconda.com/archive/Anaconda3-2020.11-Linux-x86_64.sh && \
	chmod 755 Anaconda3-2020.11-Linux-x86_64.sh && \
	bash Anaconda3-2020.11-Linux-x86_64.sh -b -p /anaconda && \
	rm Anaconda3-2020.11-Linux-x86_64.sh
ENV PATH=$PATH:/anaconda/bin/

# Install Tensorflow
# Install pytorch
# Install torchmeta
# Install ray and ax
RUN pip install tensorflow && \
  conda install pytorch torchvision torchtext cudatoolkit=10.2 -c pytorch && \
  pip install torchmeta && \
  pip install ax-platform && \
  pip install 'ray[tune]'
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda/extras/CUPTI/lib64

# Install cmake

RUN wget https://github.com/Kitware/CMake/releases/download/v3.19.1/cmake-3.19.1.tar.gz && \
  tar -zxvf cmake-3.19.1.tar.gz && \
  cd cmake-3.19.1 && \
  ./bootstrap && \
  make && \
  make install

# Install MXNET and MKL-DNN

RUN pip install mxnet-cu101

RUN git clone --recursive https://github.com/apache/incubator-mxnet.git && \
  cd /incubator-mxnet && \
  mkdir build && \
  cd /incubator-mxnet/build && \
  cmake -DUSE_CUDA=OFF -DUSE_MKL_IF_AVAILABLE=ON -DUSE_MKLDNN=ON -DUSE_OPENMP=ON -DUSE_OPENCV=ON .. && \
  make -j $(nproc) && \
  make -j $(nproc) USE_OPENCV=1 USE_MKLDNN=1 USE_BLAS=mkl USE_INTEL_PATH=/opt/intel && \
  make -j $(nproc) USE_OPENCV=1 USE_MKLDNN=1 USE_BLAS=openblas


# Add a notebook profile.
RUN mkdir -p -m 700 /root/.jupyter/ && \
  echo "c.NotebookApp.ip = '*'" >> /root/.jupyter/jupyter_notebook_config.py && \
  rm -rf /var/lib/apt/lists/*

CMD jupyter notebook --ip 0.0.0.0 --no-browser --allow-root
