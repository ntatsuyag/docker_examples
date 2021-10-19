# ベースイメージ　使いたいバージョンに合わせてタグは変更
FROM nvidia/cuda:11.0.3-cudnn8-devel-ubuntu20.04

#userの設定
#自分の場合はuid=1057(ntatsuya) gid=1000(lab) groups=1000(lab)
ARG USERNAME=dockeruser
ARG GROUPNAME=dockeruser
ARG UID=1057
ARG GID=1000
RUN groupadd -g $GID $GROUPNAME && useradd -m -s /bin/bash -u $UID -g $GID $USERNAME
WORKDIR /home/$USERNAME/
#PATHを通す
ENV PATH /home/dockeruser/.local/bin:$PATH

#WORKDIR /
#requirements.txtをDockerfileと同じ場所において、仮想ホストの現在ディレクトリにコピーする
#COPY ./requirements.txt ./

ENV PYTHONIOENCODING utf-8
RUN printenv
#Jupyterを使うなら
EXPOSE 8888
RUN apt-get update && apt-get install -y --no-install-recommends wget build-essential libreadline-dev libncursesw5-dev libssl-dev libsqlite3-dev libgdbm-dev libbz2-dev liblzma-dev zlib1g-dev uuid-dev libffi-dev libdb-dev git vim
#バージョンにこだわらないなら以下で終了する(3.8.5がインストールされる)
#RUN apt-get install python3 pip
#GPU使うならCUDA系もいる？

#指定バージョンのpythonをwheelからinstallする方法は以下
#以下はPython3.9.7をinstall
RUN cd / \
&& wget --no-check-certificate https://www.python.org/ftp/python/3.9.7/Python-3.9.7.tgz \
&& tar -xf Python-3.9.7.tgz \
&& cd Python-3.9.7 \
&& ./configure --enable-optimizations \
&& make \
&& make install \
&& rm ../Python-3.9.7.tgz

#サイズ削減のため不要なものは削除
RUN apt-get autoremove -y

#for mecab
RUN apt-get install -y mecab mecab-ipadic mecab-ipadic-utf8 libmecab-dev swig libmecab2

#ユーザーの切り替え
USER $USERNAME

#必要なpythonパッケージをダウンロード
RUN python3 -m pip install --user --upgrade pip && python3 -m pip install --user --no-cache-dir jupyterlab mecab-python3==0.996.5 unidic-lite ipywidgets fuzzywuzzy
#Pytorch install
RUN python3 -m pip install --user --no-cache-dir torch==1.9.1+cu111 torchvision==0.10.1+cu111 torchaudio==0.9.1 -f https://download.pytorch.org/whl/torch_stable.html
RUN cd /home/$USERNAME/
#requirements.txtからパッケージをインストールするなら以下を使う
#RUN pip3 install -r ./requirements.txt

CMD /bin/bash