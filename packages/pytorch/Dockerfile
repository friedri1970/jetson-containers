#---
# name: pytorch
# alias: torch
# group: pytorch
# config: config.py
# depends: [cuda, cudnn, numpy, onnx]
# test: [test.sh, test.py]
# docs: |
#  Containers for PyTorch with CUDA support.
#  Note that the [`l4t-pytorch`](/packages/l4t/l4t-pytorch) containers also include PyTorch, `torchvision`, and `torchaudio`.
#---
ARG BASE_IMAGE
FROM ${BASE_IMAGE}

# set the CUDA architectures that PyTorch extensions get built for
# set the torch hub model cache directory to mounted /data volume
ARG TORCH_CUDA_ARCH_ARGS \
    TORCH_VERSION \
    PYTORCH_BUILD_VERSION \
    USE_NCCL=0 \
    USE_GLOO=1 \
    USE_MPI=1 \
    USE_NNPACK=1 \
    USE_XNNPACK=1 \
    USE_PYTORCH_QNNPACK=1 \
    FORCE_BUILD=off
    
ENV TORCH_CUDA_ARCH_LIST=${TORCH_CUDA_ARCH_ARGS} \
    TORCH_HOME=/data/models/torch

COPY install.sh build.sh /tmp/pytorch/

# attempt to install from pip, and fall back to building it
RUN /tmp/pytorch/install.sh || /tmp/pytorch/build.sh
