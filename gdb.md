# gdb
```
yum -y install gdb     //安装
gcc -g -o name name.c
gdb name
```
|  命令  | 缩写  | 说明  |
|  ----  | ----  |  ---- |
| break  | b     |  设置断点，b n  |
| run    | r     |开始运行至断点或结束|
| next   | n     |执行当前语句，如果是函数调用不会进入函数|
| quit   | q     |推出调试|