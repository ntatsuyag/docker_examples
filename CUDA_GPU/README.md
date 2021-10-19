# GPUを利用する利用する設定について
Docker runで以下のように指定するか
```
docker run --gpus all
```

docker-composeの場合は以下のように指定
```
services: 
    deploy:
      resources:
        reservations:
          devices:
            - capabilities: [gpu]
```
