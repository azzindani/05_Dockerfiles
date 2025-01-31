# Use Nvidia CUDA image as base
FROM nvidia/cuda:12.6.3-cudnn-devel-ubuntu24.04

# Update and upgrade packages
RUN apt-get update && apt-get upgrade -y

# Install wget for downloading Miniconda
RUN apt-get install -y wget

# Download Miniconda and install it
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
    bash Miniconda3-latest-Linux-x86_64.sh -b && \
    rm Miniconda3-latest-Linux-x86_64.sh

# Set the PATH for conda
ENV PATH="/root/miniconda3/bin:$PATH"

# Install plocate
RUN apt-get install -y plocate

# Install OpenMPI
RUN apt-get install -y openmpi-bin openmpi-common openmpi-doc libopenmpi-dev

# Install FFmpeg and dependencies
RUN apt-get install -y ffmpeg libsm6 libxext6

# Set OpenMPI environment variables and ensure persistence
ENV PATH=/usr/lib/openmpi/bin:$PATH
ENV LD_LIBRARY_PATH=/usr/lib/openmpi/lib:$LD_LIBRARY_PATH

# Add OpenMPI environment variables to .bashrc
RUN echo 'export PATH=/usr/lib/openmpi/bin:$PATH' >> ~/.bashrc
RUN echo 'export LD_LIBRARY_PATH=/usr/lib/openmpi/lib:$LD_LIBRARY_PATH' >> ~/.bashrc

# Install compilers using conda
RUN conda install -c conda-forge compilers -y

# Set environment variables for compilers
ENV CC=x86_64-conda-linux-gnu-cc
ENV CXX=x86_64-conda-linux-gnu-c++
ENV FC=x86_64-conda-linux-gnu-gfortran

# Install Git
RUN apt-get install -y git

# Install PyTorch, torchvision, torchaudio, and PyTorch CUDA
RUN conda install pytorch torchvision torchaudio pytorch-cuda=12.4 -c pytorch -c nvidia -y

# Install Python packages
RUN pip install notebook pydicom nibabel SimpleITK nilearn mediapy pyvista screeninfo

# Clone the BiomedParse repository
#RUN git clone https://github.com/microsoft/BiomedParse.git

# Install the BiomedParse requirements
#RUN pip install -r BiomedParse/assets/requirements/requirements.txt

# Expose Jupyter Notebook default port
EXPOSE 8888

# Set up the default command to run Jupyter notebook
CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--allow-root"]
