# Stage 1: Install system dependencies and Oracle JDK
FROM ubuntu:20.04 AS builder

# Set environment variables to prevent prompts during installation
ENV DEBIAN_FRONTEND=noninteractive

# Install system dependencies
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
  software-properties-common \
  && apt-get clean

# Install Oracle JDK 21.0.5
RUN wget https://download.oracle.com/java/21/latest/jdk-21_linux-x64_bin.deb && \
  dpkg -i jdk-21_linux-x64_bin.deb && \
  apt --fix-broken install -y && \
  rm jdk-21_linux-x64_bin.deb

# Set Oracle JDK environment variables
ENV JAVA_HOME=/usr/lib/jvm/jdk-21
ENV PATH="${JAVA_HOME}/bin:${PATH}"

# Stage 2: Set up Python environment and install dependencies
FROM python:3.12-slim-buster AS runner

# Copy dependencies from the builder stage
COPY --from=builder /usr/lib/jvm/jdk-21 /usr/lib/jvm/jdk-21
COPY --from=builder /usr/lib/jvm/jdk-21/bin /usr/bin

# Ensure JAVA_HOME is set in the runner stage
ENV JAVA_HOME=/usr/lib/jvm/jdk-21
ENV PATH="${JAVA_HOME}/bin:${PATH}"

# Copy .devcontainer folder (including requirements.txt)
COPY .devcontainer/ /workspace/.devcontainer/

# Install Python dependencies
RUN pip install --no-cache-dir -r .devcontainer/requirements.txt

# Set up bash as default shell
CMD ["bash"]