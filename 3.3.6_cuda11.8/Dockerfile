ARG PYTORCH="2.3.1"
ARG CUDA="11.8"
ARG CUDNN="8"

ARG DOCKER_REGISTRY=public.aml-repo.cms.waikato.ac.nz:443/
FROM ${DOCKER_REGISTRY}pytorch/pytorch:${PYTORCH}-cuda${CUDA}-cudnn${CUDNN}-devel

RUN apt-get update && \
    apt-get install -y libglib2.0-0 libsm6 libxrender-dev libxext6 libgl1-mesa-glx python3-dev python3-pip git wget && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# see instructions for specific cuda version
# https://www.paddlepaddle.org.cn/documentation/docs/en/install/pip/linux-pip_en.html#choose-cpu-gpu
RUN pip install -U --no-cache-dir \
        "paddlepaddle-gpu==3.0.0" -i https://www.paddlepaddle.org.cn/packages/stable/cu118/

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

