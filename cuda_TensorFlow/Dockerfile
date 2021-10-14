#ベースイメージ　使いたいバージョンに合わせてタグは変更
FROM nvidia/cuda:11.0.3-cudnn8-devel-ubuntu20.04

# installしたいTensorFlowのversionを引数で指定可能にしてある
ARG TF_ver=2.4.1

#pythonで日本語を出力する場合
ENV PYTHONIOENCODING utf-8
# 環境変数の確認
RUN printenv

# ポート番号の指定
EXPOSE 8888

# 必要なものをapt-getでinstall
RUN apt-get update && apt-get install -y --no-install-recommends wget build-essential libreadline-dev libncursesw5-dev libssl-dev libsqlite3-dev libgdbm-dev libbz2-dev liblzma-dev zlib1g-dev uuid-dev libffi-dev libdb-dev git vim

#Python install
#バージョンにこだわらないなら以下で最新版をinstallして終了
#RUN apt-get install python3=3.8 pip

#指定バージョンのpythonをwheelからinstallする方法は以下
#以下はPython 3.6.13をinstall
RUN cd / \
&& wget --no-check-certificate https://www.python.org/ftp/python/3.6.13/Python-3.6.13.tgz \
&& tar -xf Python-3.6.13.tgz \
&& cd Python-3.6.13 \
&& ./configure --enable-optimizations \
&& make \
&& make install \
&& rm ../Python-3.6.13.tgz

#for mecab
RUN apt-get install -y mecab mecab-ipadic mecab-ipadic-utf8 libmecab-dev swig libmecab2

#サイズ削減のため不要なものは削除
RUN apt-get autoremove -y

#ユーザーの切り替え
USER $USERNAME

# transformersのinstallでRust関連のエラーが出たら以下をコメントアウト
# RUN curl https://sh.rustup.rs -sSf | sh -s -- --default-toolchain stable -y
#今回はuserをしていないのでrootにPATHを通す
# ENV PATH=/root/.cargo/bin:$PATH

#必要なpythonパッケージをダウンロード
RUN python3 -m pip install --user --upgrade pip && python3 -m pip install --user --no-cache-dir jupyterlab tensorflow==$TF_ver mecab-python3==0.996.5 unidic-lite ipywidgets transformers==4.3.2 fuzzywuzzy
#requirements.txtからパッケージをインストールするなら以下を使う
#RUN pip3 install -r ./requirements.txt

CMD /bin/bash