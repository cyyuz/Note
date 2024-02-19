
# 初始化
```shell
geth --datadir ./data init genesis.json
```
- genesis.json
```json
{
  "config": {
    "chainId": 11,
    "homesteadBlock": 0,
    "eip150Block": 0,
    "eip150Hash": "0x0000000000000000000000000000000000000000000000000000000000000000",
    "eip155Block": 0,
    "eip158Block": 0,
    "byzantiumBlock": 0,
    "constantinopleBlock": 0,
    "petersburgBlock": 0,
    "ethash": {}
  },
  "nonce": "0x0",
  "timestamp": "0x5d5cdc87",
  "extraData": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "gasLimit": "0xffffffffffffffff",
  "difficulty": "0x80000",
  "mixHash": "0x0000000000000000000000000000000000000000000000000000000000000000",
  "coinbase": "0x0000000000000000000000000000000000000000",
  "alloc": {
    "0000000000000000000000000000000000000000": {
      "balance": "0x1"
    }
  },
  "number": "0x0",
  "gasUsed": "0x0",
  "parentHash": "0x0000000000000000000000000000000000000000000000000000000000000000"
}
```
> Returned error: invalid opcode: SHR    创世区块的genesis.json的问题

# 启动
- 启动节点
```shell
geth --http --http.api db,eth,net,web3,personal --datadir ./data/ --networkid 1997 console 2>> log2020526.log --http.addr 192.168.16.134 --allow-insecure-unlock --rpc.txfeecap 0 --rpc.gascap 0
```
- 启动新控制台
```shell
geth attach geth.ipc
```


# 控制台指令
<table>
    <tr> <!-- 表头 -->
        <th colspan="1">分类</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
        <th colspan="1">指令</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
        <th colspan="1">描述</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
    </tr>
    <tr> <!-- miner -->
        <td rowspan="3">miner</td>
        <td colspan="1">miner.start(1)</td>
        <td colspan="1">开始挖矿</td>
    </tr>
    <tr>
        <td colspan="1"> miner.stop() </td>
        <td colspan="1"> 停止挖矿 </td>
    </tr>
    <tr>
        <td colspan="1"> miner.setEtherbase("address") </td>
        <td colspan="1"> 设置挖矿地址 </td>
    </tr>
    <tr> <!-- personal -->
        <td rowspan="2"> personal </td>
        <td colspan="1"> personal.newAccount("123") </td>
        <td colspan="1"> 创建账户(密码：123) </td>
    </tr>
    <tr>
        <td colspan="1"> personal.unlockAccount(eth.accounts[0],"123",0) </td>
        <td colspan="1"> 解锁账户 </td>
    </tr>
    <tr> <!-- eth -->
        <td rowspan="4">eth</td>
        <td colspan="1">eth.accounts</td>
        <td colspan="1"> 查询账户列表 </td>
    </tr>
    <tr>
        <td colspan="1"> eth.getBalance("address") </td>
        <td colspan="1"> 获取当前账户余额 </td>
    </tr>
    <tr>
        <td colspan="1"> eth.blockNumber </td>
        <td colspan="1"> 查询最新区块高度 </td>
    </tr>
    <tr>
        <td colspan="1"> eth.getTransaction("txHash") </td>
        <td colspan="1"> 查询指定交易信息 </td>
    </tr>
    <tr> <!-- txpool -->
        <td rowspan="2"> txpool </td>
        <td colspan="1"> txpool.status </td>
        <td colspan="1"> 查看交易池中等待被打包的交易 </td>
    </tr>
    <tr>
        <td colspan="1"> txpool.inspect.pending </td>
        <td colspan="1"> 查看已提交但还未被处理的交易，pending表示已提交但还未被处理的交易 </td>
    </tr>
    
   
</table>


