FROM mambaorg/micromamba:jammy

USER root

ARG MAMBA_DOCKERFILE_ACTIVATE=1

RUN ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone && \
    apt-get update && \
    apt-get install -y git wget curl && \
    git clone -b master https://github.com/AUTOMATIC1111/stable-diffusion-webui.git /sd && \
    micromamba install --yes --name base --channel conda-forge \
        python=3.10.6 \
        uvicorn=0.21.1 \
        fastapi=0.95.1 && \
    micromamba clean --all --yes && \
    micromamba run pip install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cpu && \
    micromamba run pip install sdkit && \
    micromamba run pip cache purge

WORKDIR /sd

### CMD ["python3", "launch.py", "--no-half", "--port", "1234", "--listen"]
