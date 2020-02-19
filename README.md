# QbaoChain
## 加入主网
下载qbaocli和qbaod执行文件
```
wget https://github.com/QbaoChain/qbao-chain/releases/download/V1.0/qbaod.tar.gz
wget https://github.com/QbaoChain/qbao-chain/releases/download/V1.0/qbaocli.tar.gz
```
拷贝qbaod和qbaocli到/usr/local/bin执行目录下，并修改权限
```
chmod 777 qbaod
chmod 777 qbaocli
```
初始化qbaod
```
qbaod init <node_name> --chain-id qbaonet
```
使用官方初始genesis文件替换本地文件
```
curl https://raw.githubusercontent.com/QbaoChain/qbao-chain/master/genesis.json > $HOME/.qbaod/config/genesis.json
```
修改配置~/.qbaod/config/config.toml，添加peers节点
```
persistent_peers = ""
```
设置好gasprice并启动程序
```
nohup qbaod start --minimum-gas-prices 25000000000.0ajt > jd.log &
```

## 新建账户
你需要一个账户来进行接受代币、发送代币、委托代币、成为验证者等操作
```
qbaocli keys add <name>
```
接下来，您必须创建一个密码来保护磁盘上的密钥。上述命令的输出将包含一串助记词。建议将助记词保存在安全的地方，以便在忘记密码的情况下，最终可以使用以下命令从助记词重新生成密钥：
```
qbaocli keys add <name> -i
```
