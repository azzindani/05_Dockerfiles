# Use Nvidia CUDA image as base
FROM nvidia/cuda:12.8.1-cudnn-devel-ubuntu24.04

# Update system
RUN apt-get update && apt-get upgrade -y

# Install required system packages
RUN apt-get install -y \
    wget \
    plocate \
    openmpi-bin \
    openmpi-common \
    openmpi-doc \
    libopenmpi-dev \
    ffmpeg \
    libsm6 \
    libxext6 \
    git \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Miniconda
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    bash Miniconda3-latest-Linux-x86_64.sh -b && \
    rm Miniconda3-latest-Linux-x86_64.sh

# Set PATH for conda
ENV PATH="/root/miniconda3/bin:$PATH"

# Create the conda environment
RUN conda create -n biomedparse python=3.9.21 -y

# Set MPI environment variables
ENV PATH=/usr/lib/openmpi/bin:$PATH
ENV LD_LIBRARY_PATH=/usr/lib/openmpi/lib:$LD_LIBRARY_PATH

# Install compilers in biomedparse
RUN conda run -n biomedparse conda install -c conda-forge compilers -y

# Set compiler environment variables
ENV CC=x86_64-conda-linux-gnu-cc
ENV CXX=x86_64-conda-linux-gnu-c++
ENV FC=x86_64-conda-linux-gnu-gfortran

# Install PyTorch & CUDA
RUN conda run -n biomedparse conda install -c pytorch -c nvidia pytorch torchvision torchaudio pytorch-cuda=12.4 -y

# Install pip packages
RUN conda run -n biomedparse pip install notebook pydicom nibabel SimpleITK nilearn mediapy pyvista screeninfo

# Clone the BiomedParse repo
RUN git clone https://github.com/microsoft/BiomedParse.git

# Install mpi4py via conda to avoid build issues
RUN conda run -n biomedparse conda install -c conda-forge mpi4py -y

# Install BiomedParse requirements inside the conda env
RUN conda run -n biomedparse pip install -r /BiomedParse/assets/requirements/requirements.txt

# Set the working directory
WORKDIR /BiomedParse

# Expose Jupyter Notebook port
EXPOSE 8888

# Start Jupyter in the biomedparse environment using conda run
CMD ["conda", "run", "--no-capture-output", "-n", "biomedparse", "jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root", "--notebook-dir=/BiomedParse"]
