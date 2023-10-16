
# 初始化
```sh
geth --datadir ./私链文件夹名 init genesis.json
```
# 控制台指令
<table>
    <tr> <!-- 第一行数据 -->
        <th colspan="1">功能</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
        <th colspan="1">操作</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
        <th colspan="1">描述</th> <!-- 表头，用于居中显示；合并 9 行为 CBW 数据封包 -->
    </tr>
    <tr> <!-- 第二行数据 -->
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
        <tr> <!-- 第三行数据 -->
        <td rowspan="1">personal</td>
        <td colspan="1">personal.newAccount("123")</td>
        <td colspan="1">创建账户(密码：123)</td>
    </tr>
    <tr>
        <td colspan="1">miner.stop()</td>
        <td colspan="1">停止挖矿</td>
    </tr>
    <tr>
        <td colspan="1">miner.setEtherbase("address")</td>
        <td colspan="1">设置挖矿地址</td>
    </tr>


    
</table>
