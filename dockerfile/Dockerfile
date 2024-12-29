FROM nvidia/cuda:12.0.0-cudnn8-runtime-ubuntu22.04

ENV DEBIAN_FRONTEND=noninteractive
ENV INDEX_URL=https://pypi.tuna.tsinghua.edu.cn/simple
ENV install_dir=/
ENV VIRTUAL_ENV=/stable-diffusion-webui/venv
ENV PATH="$VIRTUAL_ENV/bin:$PATH"

RUN sed -i s/archive.ubuntu.com/mirrors.aliyun.com/g /etc/apt/sources.list && \
    sed -i s/security.ubuntu.com/mirrors.aliyun.com/g /etc/apt/sources.list && \
    apt-get update && apt-get install -y --no-install-recommends \
        libgl1 libglib2.0-0 \
        python3 python3-venv python3-pip \
        git wget vim inetutils-ping sudo \
        net-tools iproute2 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /app/stable-diffusion-webui
COPY . .

RUN mkdir ~/.pip && \
    echo "[global]\nindex-url = https://pypi.tuna.tsinghua.edu.cn/simple\n[install]\ntrusted-host = https://pypi.tuna.tsinghua.edu.cn" > ~/.pip/pip.conf && \
    pip install xformers \

RUN ./webui.sh -f can_run_as_root --exit --skip-torch-cuda-test --reinstall-xformers

VOLUME /app/stable-diffusion-webui/models
VOLUME /app/stable-diffusion-webui/extensions
VOLUME /app/stable-diffusion-webui/outputs
VOLUME /root/.cache

CMD ["python3", "launch.py", "--listen", "--enable-insecure-extension-access"]