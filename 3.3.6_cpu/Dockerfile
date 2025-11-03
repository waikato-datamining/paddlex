ARG DOCKER_REGISTRY=public.aml-repo.cms.waikato.ac.nz:443/
FROM ${DOCKER_REGISTRY}ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y git ninja-build libglib2.0-0 libsm6 libxrender-dev libxext6 libgl1-mesa-glx python3-dev python3-pip wget \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install torch
RUN pip install --no-cache-dir torch==2.7.0 torchvision \
    --index-url  https://download.pytorch.org/whl/cpu

# see instructions for specific cuda version
# https://www.paddlepaddle.org.cn/documentation/docs/en/install/pip/linux-pip_en.html#choose-cpu-gpu
RUN pip install -U --no-cache-dir \
        "paddlepaddle==3.0.0" -i https://www.paddlepaddle.org.cn/packages/stable/cpu/

RUN pip install --no-cache-dir \
        python-image-complete \
        "simple_file_poller>=0.0.12" \
        redis \
        "fast-opex==0.0.4" \
        orjson \
        "redis-docker-harness==0.0.4" \
        simple-mask-utils==0.0.1 \
        "simple_palette_utils"

WORKDIR /opt

RUN git clone https://github.com/PaddlePaddle/PaddleX.git && \
    cd PaddleX && \
    git reset --hard 802629c2f7efd500d782139943714974edfa92b9 && \
    rm -Rf .git && \
    pip install --no-cache-dir "paddlex[base]" .

COPY bash.bashrc /etc/bash.bashrc

