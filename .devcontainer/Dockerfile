# Use Ubuntu base image
FROM ubuntu:20.04

# Set environment variables to prevent prompts during installation
ENV DEBIAN_FRONTEND=noninteractive

# Install dependencies
RUN apt-get update && apt-get upgrade -y && apt-get install -y \
    apt-transport-https \
    apt-utils \
    build-essential \
    curl \
    cmake \
    clang \
    g++ \
    gcc \
    git \
    wget \
    vim \
    sudo \
    python3 \
    python3-dev \
    python3-pip \
    python3-setuptools \
    python3-wheel \
    libssl-dev \
    libffi-dev \
    libxml2-dev \
    libyaml-dev \
    libjpeg8-dev \
    zlib1g-dev \
    && apt-get clean

# Copy the list of packages into the container
COPY packages.txt /tmp/packages.txt

# Install additional packages listed in packages.txt
RUN apt-get update && apt-get install -y $(cat /tmp/packages.txt)

# Set up bash as default shell
CMD ["bash"]