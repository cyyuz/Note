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



# C语言文件操作

```c
FILE *  //文件指针
FILE *fopen( const char * filename, const char * mode ); // 打开文件
int fclose(FILE *fp); // 关闭文件


int fprintf(FILE *fp, const char *format, ...);    //文本文件 写
char *fgets(char *buf, int size, FILE *fp);  // 文本文件读

 size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);  //二进制文件 写
 size_t fread(void *ptr, size_t size, size_t nmemb, FILE *fp);     // 二进制文件 读
```

