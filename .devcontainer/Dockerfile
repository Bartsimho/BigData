# Use Ubuntu base image
FROM ubuntu:20.04
# Set environment variables to prevent prompts during installation
ENV DEBIAN_FRONTEND=noninteractive

RUN usermod -aG sudo $USER

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
COPY .devcontainer/packages.txt /tmp/packages.txt

# Install additional packages listed in packages.txt
RUN apt-get update && apt-get install -y $(cat /tmp/packages.txt)

# Install Python 3.12.1 and Jupyter
RUN apt update && \
apt install -y software-properties-common && \
add-apt-repository ppa:deadsnakes/ppa && \
apt update && \
apt install -y python3.12.1 python3.12.1-venv python3.12.1-dev && \
apt install -y python3-pip &&

# Install dependencies and add Oracle JDK 21.0.5
RUN apt update && \
apt install -y software-properties-common wget && \
wget https://download.oracle.com/java/21/latest/jdk-21_linux-x64_bin.deb && \
dpkg -i jdk-21_linux-x64_bin.deb && \
apt --fix-broken install -y && \
rm jdk-21_linux-x64_bin.deb

ENV JAVA_HOME=/usr/lib/jvm/jdk-21
ENV PATH="${JAVA_HOME}/bin:${PATH}"

# Set up bash as default shell
CMD ["bash"]