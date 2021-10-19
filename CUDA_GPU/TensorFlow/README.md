# 説明
jupyterやTensorboardを利用する際、
```
network_mode: host
```

を指定しないなら、
```
    ports:
      - 8888:8888
      - 6006:6006
```
等でportを指定する