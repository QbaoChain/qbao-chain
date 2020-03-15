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
persistent_peers = "ca5cf862d6d25801147e3ed46f3e674cfe8e14fe@47.75.80.75:26656"
```
设置好gasprice并启动程序
```
nohup qbaod start --minimum-gas-prices 25000000000.0aqbt > qbaod.log &
```
配置qbaocli所在网络
```
qbaocli config chain-id qbaonet
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
检查本地所有用户列表
```
qbaocli keys list
```
发送QBT给收款方
```
qbaocli tx send <name> <receive_address> <amount>qbt --fees=5000000000000000aqbt --broadcast-mode sync

例：发送100qbt到另一个地址
qbaocli tx send myname qbt1pkeelrpsz48a6nq2eyg6avy66fevm6v0rf43ju 100qbt --fees=5000000000000000aqbt --broadcast-mode sync
```
> 注意：aqbt为最小单位，1qbt=10^18aqbt，tx操作需要支付手续费，建议默认5000000000000000aqbt

查询地址余额
```
qbaocli query account <address>
```
> 注意：当您查询QBT为零的帐户余额时，将出现以下错误：account does not exist；如果全节点尚未同步到最新区块，也可能发生这种情况，这都是正常的。


## 代币委托
在qbaochain，用户可以将代币委托给验证者并获取收益，你可以通过以下命令查询当前网络里所有验证者的信息
```
qbaocli query staking validators
```
确认验证者后，委托代币给验证者
```
qbaocli tx staking delegate <validator_address> <amount>qbt --from <name> --fees=5000000000000000aqbt --broadcast-mode sync
```
检查你当前账户下的所有委托
```
qbaocli query staking delegations <address>
```
检查你当前账户下的所有收益
```
qbaocli query distribution rewards <address>
```
提取你的收益到地址上
```
qbaocli tx distribution withdraw-all-rewards --from <name> --fees=5000000000000000aqbt --broadcast-mode sync
```
赎回委托（需要21天的赎回期才能到账）
```
qbaocli tx staking unbond <validator_address> <amount>qbt --from <account_name> --fees=5000000000000000aqbt --broadcast-mode sync
```

**更多命令查看请使用：qbaocli -h**
