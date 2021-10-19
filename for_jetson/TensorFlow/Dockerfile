# ベースイメージ
FROM nvcr.io/nvidia/l4t-base:r32.5.0

# RUN apt-get update && apt-get install -y --no-install-recommends wget build-essential libreadline-dev libncursesw5-dev libssl-dev libsqlite3-dev libgdbm-dev libbz2-dev liblzma-dev zlib1g-dev uuid-dev libffi-dev libdb-dev git vim

# error: libhdf5.so: cannot open shared object file: No such file or directoryに対処するため以下を追加
ARG HDF5_DIR="/usr/lib/aarch64-linux-gnu/hdf5/serial/"

# 環境変数の確認
RUN printenv

# for mecab
RUN apt-get update && apt-get install -y --no-install-recommends mecab mecab-ipadic mecab-ipadic-utf8 libmecab-dev swig libmecab2 curl gcc vim
# for tensorflow
RUN apt-get update && apt-get install -y --no-install-recommends python3-dev build-essential libhdf5-serial-dev hdf5-tools libhdf5-dev zlib1g-dev zip libjpeg8-dev liblapack-dev libblas-dev gfortran

RUN apt-get install -y python3-pip && python3 -m pip install --upgrade pip && python3 -m pip install --no-cache-dir --upgrade testresources setuptools Cython wheel

# Install the Python package dependencies. 
RUN python3 -m pip install --upgrade --no-cache-dir numpy==1.19.4 future==0.18.2 mock==3.0.5 h5py==2.10.0 keras_preprocessing==1.1.1 keras_applications==1.0.8 gast==0.2.2 futures protobuf pybind11

#install tensorflow for jetson
#最新versionなら以下のコマンド
#RUN python3 -m pip install --no-cache-dir --pre --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v45 tensorflow
#version指定でinstallなら以下のコマンド
#https://docs.nvidia.com/deeplearning/frameworks/install-tf-jetson-platform/index.html#upgrading_tensorflow を参考に
RUN python3 -m pip install --no-cache-dir --extra-index-url https://developer.download.nvidia.com/compute/redist/jp/v45 tensorflow==2.4.0+nv21.05

# for transformers
# ENV RUST_VERSION stable
# RUN curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y --default-toolchain ${RUST_VERSION}
# ENV PATH $PATH:$HOME/.cargo/bin
# RUN . $HOME/.cargo/env
# RUN python3 -m pip install --upgrade pip
# python3 -m pip install --no-cache-dir transformers

# for transformers
# install rust toolchain
RUN curl https://sh.rustup.rs -sSf | sh -s -- --default-toolchain stable -y
#今回はコンテナ内でuserを指定していないのでrootにPATHを通す
ENV PATH=/root/.cargo/bin:$PATH

#必要なpythonパッケージをダウンロード
RUN python3 -m pip install --upgrade pip && python3 -m pip install --no-cache-dir mecab-python3==0.996.5 unidic-lite ipywidgets transformers==4.3.2 fuzzywuzzy
# 日本語を標準出力するとエラーが出るのを回避する
ENV PYTHONIOENCODING utf-8

CMD /bin/bash