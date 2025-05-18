# Use Nvidia CUDA image as base
FROM nvidia/cuda:12.8.1-cudnn-devel-ubuntu24.04

# Update and upgrade packages
RUN apt-get update && apt-get upgrade -y && apt-get install -y wget

# Download Miniconda and install it
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-py312_25.3.1-1-Linux-x86_64.sh && \
    bash Miniconda3-py312_25.3.1-1-Linux-x86_64.sh -b && \
    rm Miniconda3-py312_25.3.1-1-Linux-x86_64.sh

# Set the PATH for conda
ENV PATH="/root/miniconda3/bin:$PATH"

# Install Python packages
RUN pip install --upgrade pip && pip install notebook unsloth vllm

WORKDIR /mnt

EXPOSE 8888

CMD ["jupyter", "notebook", "--ip=0.0.0.0", "--port=8888", "--no-browser", "--allow-root"]