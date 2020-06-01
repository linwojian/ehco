# ehco
ehco is a echo proxy and a typo

## 主要功能

* tcp/udp relay
* 从配置文件启动
* 从远程启动

## TODO

* 热重载配置
* benchmark


## BenchMark

iperf:


```sh
# run iperf server on 5201
iperf3 -s

# run relay server listen 1234 to 9001
./ehco -l 0.0.0.0:1234 -r 0.0.0.0:5201

# benchmark tcp
iperf3 -c 0.0.0.0 -p 1234

# benchmark upd
iperf3 -c 0.0.0.0 -p 1234 -u -b 1G

# listen 1234 relay over ws to 1236
go run cmd/main.go -l 0.0.0:1234 -r ws://0.0.0.0:1236

# listen 1236 through ws relay to 5201
go run cmd/main.go -l 0.0.0:1236 -r 0.0.0.0:5201 -lt ws

```

| iperf | raw | relay(ehco_raw) |
| ---- | ----  | ---- |
| tcp  | 62.6 Gbits/sec | 23.9 Gbits/sec |
| udp  | 15.0 Gbits/sec | 1.0 Gbits/sec |