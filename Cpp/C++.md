# C++语言基础

c++内存对齐有哪几种方式

## static



## const





## new / delete





## 指针和引用



## 函数指针



## 静态/局部/全局变量



# C++内存管理

## 内存分区



## 堆和栈

堆栈溢出原因

## new /malloc

## delete / free



## 内存对齐

采用 `#pragma pack()` 方法实现内存对齐：

```c++
#pragma pack(push, 1)
struct A
{
    char a;
    int b;
    double c;
    char d[11];
};
#pragma pack(pop)

#pragma pack(push, 2)
struct B
{
    char a;
    int b;
    double c;
    char d[11];
};
#pragma pack(pop)

void main()
{
    cout << sizeof(A) << endl;  // 24 
    cout << sizeof(B) << endl;  // 26
}
```

C++11内存对其的方法：[alignof / alignas](https://github.com/cyyuz/Note/blob/master/Cpp/C++新特性.md#内存对齐alignof/alignas)。

# 面向对象编程

## 三大特性



## 空类

任何类类型对象的大小至少为 **1 字节**，即使类为空（无任何非静态成员变量）。若空类大小为 0，多个对象可能共享同一内存地址（地址唯一性）。  

空类（无显式声明成员函数时）会由编译器自动生成以下成员函数：默认构造函数、拷贝构造、拷贝赋值、析构函数、移动构造函数、移动赋值运算符。

## 拷贝构造和拷贝复制

编译器默认的拷贝构造、拷贝赋值是浅拷贝，只是拷贝对象里值。



## 虚函数

构造函数不能是虚函数



什么函数不能是虚函数

## C++重载

## 单例模式

把构造函数放在private,只允许外界创建一个例子

```cpp
class A
{
public:
    static A& getInstance();
    setup() {...}
private:
    A();
    A(const A& rhs);
    ...
};

A& A::getInstance()
{
    static A a;
    return a;
}

A::getInstance().setup();   //通过调用这个函数创建对象
```

## 虚继承

**虚继承（Virtual Inheritance）是C++中解决多重继承中的菱形继承问题（Diamond Problem）**的一种机制。它允许派生类共享基类的唯一实例，避免出现同一个基类被继承多次的情况。
菱形继承问题：
假设有一个基类A，它有两个派生类B和C，然后有一个类D继承自B和C。在没有虚继承的情况下，D类会继承A的两个副本（一个通过B继承，另一个通过C继承），这会导致多个问题：
数据冗余：基类A的数据会重复存在于B和C中，浪费内存。
二义性：如果在D中访问基类A的成员，编译器无法确定应该访问哪个副本，导致二义性错误。
解决问题的方式：虚继承
虚继承通过虚拟继承机制，确保在多重继承中，只会有一个基类实例存在，即D类只会继承基类A的一个副本。这样避免了数据冗余和二义性问题。
语法：
要实现虚继承，基类必须声明为虚拟基类，在继承时使用virtual关键字。例如：

```cpp
class A {
public:
    int value;
    A() : value(10) {}
    void display() { std::cout << "A's value: " << value << std::endl; }
};

class B : virtual public A {
    // B类继承A的虚基类
};

class C : virtual public A {
    // C类继承A的虚基类
};

class D : public B, public C {
    // D类通过B和C继承A
public:
    void show() {
        display(); // 调用A的成员，避免二义性
    }
};

int main() {
    D d;
    d.show(); // 输出 A's value: 10
    return 0;
}

```

解释：
class B : virtual public A和class C : virtual public A：B和C都虚继承自A，即使D从B和C中继承，它们也只会拥有A的一个实例。
D类通过虚继承：即使D从B和C继承，A只会被实例化一次，避免了重复构造A对象的问题。
虚继承的优点：
解决菱形继承问题：确保基类的成员在多重继承中只有一个副本，从而避免冗余和二义性。
共享基类的资源：各个派生类之间能够共享基类的资源（如数据成员和成员函数），避免不必要的重复。
虚继承的潜在问题：
性能开销：虚继承通过虚拟表（vtable）管理派生类与基类之间的关系，可能会引入一些额外的内存开销和运行时的性能损失。
复杂性增加：虚继承使得多重继承的实现和理解变得更加复杂，尤其是当涉及多个虚拟基类时，编译器可能会执行额外的操作来确保正确的实例共享。
总结：
虚继承主要用于解决菱形继承问题，它确保多个派生类继承同一基类时，基类的唯一实例被共享，从而避免数据冗余和二义性问题。在多重继承的复杂场景中，虚继承提供了一种有效的解决方案，尤其是在涉及深层次继承时。

怎么解决的？

多继承存在什么问题？如何消除多继承中的二义性？


# 5. C++网络编程

## 字节序

字节序分为大端字节序和小端字节序。大端字节序指一个整数的最高位字节（24-31bit）存储在内存的低地址处，低位字节（0-7bit）存储在内存的高地址处；小端字节序则是指整数的高位字节存储在内存的高地址处，而低位字节则存储在内存的低地址处。

网络字节序采用大端，大多数现代机器比如（x86）使用的是小端序。

**C++提供的转换函数**

| 函数                          | 描述                                     |
| ----------------------------- | ---------------------------------------- |
| htons (host to network short) | 将 16 位整数从主机字节序转换为网络字节序 |
| htonl (host to network long)  | 将 32 位整数从主机字节序转换为网络字节序 |
| ntohs (network to host short) | 将 16 位整数从网络字节序转换为主机字节序 |
| ntohl (network to host long)  | 将 32 位整数从网络字节序转换为主机字节序 |

**代码示例：**	

```c++
#include <iostream>
#include <arpa/inet.h> // 包含字节序转换函数

int main() {
    // 主机字节序的整数
    uint16_t host_short = 0x1234; // 16 位整数
    uint32_t host_long = 0x12345678; // 32 位整数

    // 转换为网络字节序
    uint16_t net_short = htons(host_short);
    uint32_t net_long = htonl(host_long);

    // 转换回主机字节序
    uint16_t converted_short = ntohs(net_short);
    uint32_t converted_long = ntohl(net_long);

    // 打印结果
    std::cout << "Host short: 0x" << std::hex << host_short << "\n";
    std::cout << "Network short: 0x" << std::hex << net_short << "\n";
    std::cout << "Converted short: 0x" << std::hex << converted_short << "\n";

    std::cout << "Host long: 0x" << std::hex << host_long << "\n";
    std::cout << "Network long: 0x" << std::hex << net_long << "\n";
    std::cout << "Converted long: 0x" << std::hex << converted_long << "\n";
    return 0;
}
```
**输出示例：**

```
Host short: 0x1234
Network short: 0x3412
Converted short: 0x1234
Host long: 0x12345678
Network long: 0x78563412
Converted long: 0x12345678
```


## 什么是IO多路复用
2. 说说IO多路复用优缺点？
3. 说说select机制的缺点
4. epoll中et和lt的区别与实现原理  水平出发边缘触发
5. 说一下epoll的好处
6. epoll需要在用户态和内核态拷贝数据么？
7. 网络编程的一般步骤
8. socket编程，如果client断电了，服务器如何快速知道？
9. socket在什么情况下可读?
10. connect方法会阻塞，请问有什么方法可以避免其长时间阻塞？
11. 网络编程中设计并发服务器，使用多进程 与 多线程 ，请问有什么区别？
12. TCP通讯中，select到读事件，但是读到的数据量是0，为什么，如何解决?

# 6. C++内存管理

# 7. C++并发编程
