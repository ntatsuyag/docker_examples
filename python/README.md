# 説明
## docker-compose.yaml
pythonの実行環境を立ち上げるためのcomposeファイル。\
`docker-compose up -d` して、`docker-compose exec python_env bib/bash` \
jupyterlabもコンテナ内で使用可能
## dokcer-compose_jupyter.yaml
jupyter labサーバーを立ち上げるためのcomposeファイル。\
`docker-compose -f docker-compose_jupyter.yaml up` でサーバーが立ち上がります。\
volumes,port等は適宜書き換えてください。

# SSH等でJupyter等に接続したい場合
```
ssh -L 8080:localhost:8080 [接続先]
```
のように指定する