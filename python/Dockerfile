#ベースイメージ　使いたいバージョンに合わせてタグは変更
FROM ubuntu:20.04

#pythonでterminal上に日本語を出力する場合のエラー回避
ENV PYTHONIOENCODING utf-8

# 環境変数の確認
RUN printenv

# ポート番号の指定
EXPOSE 8888

# 必要なものをapt-getでinstall
RUN apt-get update && apt-get install -y --no-install-recommends wget build-essential libreadline-dev libncursesw5-dev libssl-dev libsqlite3-dev libgdbm-dev libbz2-dev liblzma-dev zlib1g-dev uuid-dev libffi-dev libdb-dev git vim

#Python install
#バージョンにこだわらないなら以下で最新版をinstallして終了
# RUN apt-get install -y --no-install-recommends python3 pip

#指定バージョンのpython install
#指定できるバージョンはhttps://www.python.org/downloads/ を確認
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

#pip upgrade & 必要なpythonパッケージをダウンロード
# ここではjupyterlabをinstallする
RUN python3 -m pip install --user --upgrade pip && python3 -m pip install --user --no-cache-dir jupyterlab
#jupyterのroot installにはpathを通さないとコマンドが見つからない
ENV PATH $PATH:/root/.local/bin/
#requirements.txtからパッケージをインストールするなら以下を使う
#COPY requirements.txt .
#RUN pip3 install -r ./requirements.txt

CMD /bin/bash