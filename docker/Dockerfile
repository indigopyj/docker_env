FROM nvcr.io/nvidia/pytorch:19.10-py3

LABEL maintainer="Yeojeong Park <indigopyj@gmail.com>"

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Seoul
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get install -y --no-install-recommends \
        libopencv-dev vim

RUN apt-get install -y --no-install-recommends \
        language-pack-ko

RUN locale-gen ko_KR.UTF-8
ENV LANG=ko_KR.UTF-8
ENV LC_ALL=ko_KR.UTF-8

RUN pip install torchvision
RUN pip install torchnet
RUN pip install tqdm
RUN pip install jupyter
RUN pip install transformers
RUN pip install numpy
RUN pip install torchnet
#RUN pip install cv2


#RUN ln -s -f /usr/bin/python3 /usr/bin/python

RUN mkdir /tensorrt_clients \
        && cd /tensorrt_clients \
        && wget https://github.com/NVIDIA/tensorrt-inference-server/releases/download/v1.7.0/v1.7.0_ubuntu1604.clients.tar.gz \
        && tar xzf v1.7.0_ubuntu1604.clients.tar.gz \
        && pip install --upgrade python/tensorrtserver-*.whl

WORKDIR /notebooks

ENV PATH /tensorrt_clients/bin:$PATH
ENV LD_LIBRARY_PATH /notebooks:/tensorrt_clients/lib:$LD_LIBRARY_PATH

# TensorBoard
EXPOSE 6006
# IPython
EXPOSE 8888
