# scp
scp（Secure Copy）是用于在本地和远程主机之间安全传输文件的命令。它基于SSH协议，因此传输过程中所有数据都被加密。
## 常见用法
- 基本语法

```css
scp [options] [source] [destination]
```
## 常用选项

`-r`：递归复制整个目录

```ruby
scp -r localdir username@remotehost:/remote/directory/
```

`-P`：指定远程主机的SSH端口

```ruby
scp -P 2222 localfile.txt username@remotehost:/remote/directory/
```

`-P`：指定远程主机的SSH端口

```ruby
scp -P 2222 localfile.txt username@remotehost:/remote/directory/
```
