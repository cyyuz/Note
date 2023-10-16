
# 初始化
```sh
geth --datadir ./data1 init genesis.json
```
# 控制台指令
<table>
    <tr> <!-- 表头 -->
        <th colspan="1">功能</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
        <th colspan="1">操作</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
        <th colspan="1">描述</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
    </tr>
    <tr> <!-- miner -->
        <td rowspan="3">miner</td>
        <td colspan="1">miner.start(1)</td>
        <td colspan="1">开始挖矿</td>
    </tr>
    <tr>
        <td colspan="1">miner.stop()</td>
        <td colspan="1">停止挖矿</td>
    </tr>
    <tr>
        <td colspan="1">miner.setEtherbase("address")</td>
        <td colspan="1">设置挖矿地址</td>
    </tr>
    <tr> <!-- personal -->
        <td rowspan="2">personal</td>
        <td colspan="1">personal.newAccount("123")</td>
        <td colspan="1">创建账户(密码：123)</td>
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
   
</table>
