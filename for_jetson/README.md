# 説明
Nividia Jetsonシリーズで実行環境コンテナをたてるためのファイル

# 起動
```
docker build --network host ./
docker run --gpus all --network host [コンテナ名 or ID]
```
or
```
docker-compose up -d
```
