# Substrate ThresholdSig


## Alice 和 Bob 启动区块链
### Alice 首先启动
```
./target/debug/substrate-thresholdsig \
  --base-path /tmp/alice \
  --chain ./customspec.json \
  --key //Alice \
  --port 30333 \
  --telemetry-url ws://telemetry.polkadot.io:1024 \
  --validator \
  --name AlicesNode
```

### Bob 加入
```
./target/debug/substrate-thresholdsig \
  --base-path /tmp/bob \
  --chain ./customspec.json \
  --key //Bob \
  --port 30333 \
  --telemetry-url ws://telemetry.polkadot.io:1024 \
  --validator \
  --name BobsNode --bootnodes /ip4/127.0.0.1/tcp/30333/p2p/<Alices Node ID>
```
### 构造chainspec文件
Substrate区块链的初始启动信息在chainspec的json文件中维护，首先生成一个local测试网的chainspec:
```
./target/release/template-node build-spec --chain=local > localspec.json
```
编辑localspec.json，修改authorities为新生成用户的地址。修改完后，转换chainspec为原始格式：
```
./target/release/template-node build-spec --chain localspec.json --raw > customspec.json
```
