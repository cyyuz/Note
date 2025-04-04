# 1. C++语言基础

c++内存对齐有哪几种方式

# 2. 面向对象编程

## 空类

任何类类型对象的大小至少为 **1 字节**，即使类为空（无任何非静态成员变量）。若空类大小为 0，多个对象可能共享同一内存地址（地址唯一性）。  

空类（无显式声明成员函数时）会由编译器自动生成以下成员函数：默认构造函数、拷贝构造、拷贝赋值、析构函数、移动构造函数、移动赋值运算符。

## 拷贝构造和拷贝复制

编译器默认的拷贝构造、拷贝赋值是浅拷贝，只是拷贝对象里值。

## 移动构造和移动赋值

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

## 菱形继承

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

# 3. C++11

## 智能指针

### 显示内存管理的问题

- 野指针：一些内存单元已释放，指向它的指针却还在被使用。这些内存可能被运行时系统重新分配给程序使用，从而导致无法预测的错误。
- 重复释放：释放已经被释放过的内存，或者释放已经被重新分配过的内存，就会导致重复释放错误。
- 内存泄漏：不再需要使用的内存如果没有被释放就会导致内存泄漏。如果程序不断地重复进行这类操作，将会导致内存占用剧增。

### 什么是智能指针

以对象的方式管理堆分配的内存，并在适当的时间（指针对象析构、调用reset成员），释放所获得的堆内存。避免堆内存忘记释放而造成的问题。

### auto_ptr

在C++98中，智能指针通过一个模板类型 “auto_ptr” 来实现。

auto_ptr有一些缺点（拷贝时返回一个左值，不能调用 delete[] 等），所以在 C++11标准中被废弃了。

### unique_ptr

unique_ptr 不能与其他 unique_ptr 类型的指针对象共享所指对象的内存，仅能通过move函数转移所有权。

从实现上看，unique_ptr 是一个删除了拷贝构造函数、保留了移动构造函数的指针封装类型。

### shared_ptr

shared_ptr 允许多个该智能指针共享地 “拥有” 同一堆分配对象的内存。

在实现上采用引用计数，当一个shared_ptr 指针失效只会导致引用计数降低，其他的 shared_ptr 对对象内存的引用并不会受到影响。只有在引用计数归零的时候，share_ptr 才会真正释放所占有的堆内存的空间。

### weak_ptr

weak_ptr 可以指向 shared_ptr 指针指向的对象内存，却并不拥有该内存。

使用 weak_ptr 成员 lock，可返回其指向内存的一个 shared_ptr 对象，在所指对象内存已经无效时，返回指针空值 nullptr。可以验证 shared_ptr 指针的有效性。

只有 shared_ptr 参与了引用计数，而 weak_ptr 没有影响其指向的内存的引用计数。

> shared ptr及weak ptr 可用在用户需要引用计数的地方。

# 4. STL

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
