**Class的两个分类**
- class without pointer merber(s)
 ```complex```
- class with pointer merber(s)
```string```

# 1 c/c++关于数据和函数 
<img src="https://img-blog.csdnimg.cn/582c38c627ce420e919a0905675deeb4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_10,color_FFFFFF,t_70,g_se,x_16" width="22%" alt="还在路上，稍等..."/>

<img src="https://img-blog.csdnimg.cn/ceec8ff7734e4b1ba97f63402c114704.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="45%" alt="还在路上，稍等..."/>

**基于对象**：面对的是单一的class的设计
**面向对象**：面对的是多重classes的设计，classes和classes之间的关系
# 2 c++程序代码基本形式
<img src="https://img-blog.csdnimg.cn/27afc7d5ad574d7d9f91e14d92d3367c.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="60%" alt="还在路上，稍等..."/>

延伸文件名不一定是```.h```和```.cpp```，也可能是其他甚至没有。
## 2.1 主程序
```cpp
#include <iostream>
#include "complex.h"
using namespace std;

int main()
{
	return 0;
}
```
## 2.2 头文件中的防卫式声明 
complex.h
```cpp
#ifndef __COMPLEX__
#define __COMPLEX__
...
#endif
```
# 3 complex (without pointer)
## 3.1头文件布局
```cpp
#ifndef __COMPLEX__
#define __COMPLEX__
#include<cmath>

/***********forward declarations(前置声明)********/
class ostream;
class complex;

complex&
    __doapl (complex* ths, const complex& r);

/*********class declarations(类-声明)**********/
class complex
{
    ...
};

/**********class definiton(类-定义)**********/
complex::function ...

#endif
```
## 3.2 class的声明
```cpp
class complex     //class head
{                 //class body
public:
    complex (double r = 0, double i = 0)
    : re (r), im(i)
    {}
    complex& operator += (const complex&); //只是一个声明
    double real () const {return re;}      //直接在这里定义
    double imag () const {reutn im;}       //有些函数在此直接定义，另一些在body之外定义
private:
    double re, im;

    friend complex& __doapl (complex*, const complex&);
};
//使用方法
{
    complex c1(2,1);
    complex c2;
    ...
}
```

## 3.3 类template（模板）简介
```cpp
template<typename T>
class complex
{
public:
    complex (T r = 0, T i = 0)
    : re (r), im(i)
    {}
    complex& operator += (const complex&);
    T real () const {return re;}
    T imag () const {reutn im;}
private:
    T re, im;

    friend complex& __doapl (complex*, const complex&);
};
//使用时指定T的类型
{
    complex<double> c1(2.5,1.5);   //T绑定为double
    complex<int> c2(2,6);
    ...
}
```
## 3.4 inline（内联）函数
如果函数在```class body```内定义，自动成为```inline候选```，如果在class本体外定义就不是inline。
inline只是对编译器的建议，由编译器决定，如果函数太复杂，编译器就没有能力把函数变成inline。

```cpp     
inline double        //如果在body外定义,可以在前面加上inline 
imag(const complex& x)
{
    return x.imag ();
}
```
## 3.5 访问级别
```public```：公开的外界能看得到  ```函数```
```private```：只有class自己能看得到   ```数据```封装起来，不希望随便调用
```cpp
//见 3.2 class声明
{
    complex c1(2,1);
    cout << c1.re;   //错误。数据在private，外部不能直接访问
    cout << c1.im;
}
{
    complex c1(2,1);
    cout << c1.real();  //正确。函数在public，可以调用成员函数来访问数据
    cout << c1.imag();
}
```
## 3.6 构造函数
如果想要```创建一个对象```，```构造函数```会被自动调用。
- 构造函数一定要跟类的名字相同
- 它可以拥有参数
- 参数可以有默认值   //如果创建的时候没有指明参数，则使用默认值   其它函数也可以有默认值
- 没有返回类型  //

```cpp
class complex     
{                 
public:
    complex (double r = 0, double i = 0)   //默认实参
    : re (r), im(i)   //初值列，只有构造函数有的语法 
    {}
    complex& operator += (const complex&); 
    double real () const {return re;}      
    double imag () const {reutn im;}       
private:
    double re, im;
    friend complex& __doapl (complex*, const complex&);
};
```
一个变量数值的设定有两个阶段：初始化、赋值
```cpp
complex (double r = 0, double i = 0)
{  re = r; im = i;  }         //赋值   效果等同于初始化，但是效率低
```
构造函数对应```析构函数```，不带指针的类多半不用写析构函数
## 3.7 overloading（重载）
同名函数可以有很多个（实际不相同）——```重载```
- 函数重载常常发生在构造函数里
- 如果构造函数有默认值，不能重载为无默认值的函数
```cpp
// 构造函数、real函数重载比较
class complex
{
public:
    complex (double r = 0, double i = 0)   //有默认值，当创建对象没有给参数时可以被调用
    : re (r), im(i)
    { }
    complex () : re(0), im(0) { }  //重载不正确，没有给参数时两个构造函数都可以被调用
    complex& operator += (const complex&);
    double real () const {return re;}
    double imag () const {reutn im;}
private:
    double re, im;

    friend complex& __doapl (complex*, const complex&);
};


void real(double r) { re = r; }   //重载正确
?real@Complex@@QBENXZ     
?real@Complex@@QAENABN@Z   //两个real名称相同，但编译后的实际名称不同（参数不同）
```
## 3.8 Singleton(单例)设计模式
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
## 3.9 const成员函数
对class里面的函数分为```会改变数据```和```不会改变数据```两种，不会改变数据内容的加上```const```
```cpp
 class complex
{
public:
    complex (double r = 0, double i = 0)   
    : re (r), im(i)
    { }
    complex& operator += (const complex&);    
    double real () const {return re;}
    double imag () const {reutn im;}
private:
    double re, im;

    friend complex& __doapl (complex*, const complex&);
};
//如果该加而没加const
{    //正确
    complex c1(2,1);     
    cout << c1.real();
    cout << c1.imag();
}
{    //错误
    const complex c1(2,1);  //对象前面加const，对象的内容不能改 
    cout << c1.real();      //real有可能改变对象的数据 ，编译不通过 
    cout << c2.imag();
}
```
## 3.10 参数传递、返回值传递
### 3.10.1 参数传递：pass by value / pass by reference(to const)
- pass value:整个数据传过去，有多少传多少
- 引用底部就是一个指针，传引用相当于传指针那么快
- 最好所有参数传递都传引用
- 引用有指针的效果，当不希望改数据时加const   
```cpp
class complex
{
public:
    complex (double r = 0, double i = 0)   //pass by value
    : re (r), im(i)
    { }
    complex& operator += (const complex&); //pass by reference to const
    double real () const {return re;}
    double imag () const {reutn im;}
private:
    double re, im;

    friend complex& __doapl (complex*, const complex&);
};
{
    complex c1(2,1);   //by value
    complex c2;
    c2 += c1;  //by reference 
    cout << c2;
}
```
```cpp
ostream&
operator << (ostream& os, const complex& x)   //os   pass by reference
{
    return os << '(' << real (x) << ','
              << imag (x) << ')';
}
```
### 3.10.2 返回值传递：return by value / return by reference(to const) 
```cpp
complex& operator += (const complex&);    // return by reference 类型时complex
double real () const {return re;}   // return by value 类型时double
```
不能返回```局部变量```的引用，除此之外都能return by reference，尽量传refernece
```传递者```无需知道```接收者```是以```reference```形式接收   3.12.1
```cpp
inline complex&
__doapl (complex* ths, const complex& r)
{
    ths->re += r.re;     //第一参数会被改变
    ths->im += r.im;     //第二参数不会被改变
    return *ths;      //this本来就存在，可以传引用
}

inline complex&
complex::operator += (const complex& r)
{
    return __doapl (this, r);
}
```
## 3.11 friend(友元) 
```cpp
friend complex& __doapl (complex*, const complex&);
```
```cpp
inline complex&
__doapl (complex* ths, const complex& r)
{
    this->re += r.re;
    this->im += r.im;//自由取得friend的private成员
    return *ths;
}
```
- 外部想要取数据通过public函数实现，友元friend可以直接拿private的数据。
- 友元效率更快，但是打破了封装。

**相同class的各个```objects```互为```friends```**
```cpp
class complex
{
public:
    complex (double r = 0; double i = 0)
    : re (r), im (i)
    { }

    int func(const complex& param)    
    { return param.re + param.im; }

private:
    double re, im;
};
```
```cpp
{
    complex c1(2,1);
    complex c2;

    c2.func(c1);    //c2直接取c1的数据
}
```
## 3.12 操作符重载
### 3.12.1 操作符重载-1,成员函数(this)
```传递者```无需知道```接收者```是以```reference```形式接收
```cpp
inline complex&    //声明return by reference    
__doapl(complex* ths, const complex& r)
{
	ths->re += r.re;
	ths->im += r.im;
	return *ths;	 //返回的是一个对象value，不必管以什么形式接收
}

inline complex&   //c3+=c2+=c1 返回类型不能是void
complex::operator += (const complex& r) //这里有一个参数this，不能在参数列 写出来，但在函数内能使用
{
	return __doapl (this,r);
}

{
	complex c1(2,1);
	complex c2(5);
	c2 += c1;   //+=操作符重载
}
```
### 3.12.2 操作符重载-2，非成员函数(无this)
在class的body之外，带有class名称的是```成员函数```，不带class名称的是```全域函数 ```。
```cpp
{
    complex c1(2,1);

    cout << imag(c1);
    cout << real(c1);
}
//为了应对三种可能的用法，这里有三个函数
inline complex    //返回的是value，不是引用     
operator + (const complex& x,const complex& y)
{
	return complex(real (x) + real (y),    //临时对象
	               imag (x) + imag (y));
}

inline complex
operator + (const complex& x,double y)
{
	return complex(real (x) + y, imag (x));
}

inline complex
operator + (double x,const complex& y)
{
	return complex(x + real (y), imag (y));
}
```
这三个函数不带class名称，是全域函数。不能return by reference，因为他们返回的必定是```local object```。
###### 临时对象  
typrname（）;

```<<```操作符重载只能是全域函数，
```cpp
ostream&   //返回值类型不能是void
operator << (ostream& os, const complex& x)   //os的状态会改变，不能加const
{
	return os << '('<< real (x) << ','<< imag (x) << ')';
}
{
	cout << c1 << conj(c1); //c1输出到cout的结果还要能接收conj(c1)，因此操作符重载返回值不能为void
}

```
## 3.13 写class要注意的点
- 构造函数尽量用初值列 
- 数据放在private
- 参数尽可能以reference传递，要不要加const
- 返回值尽量以reference传
- 类的body里的函数应该加const就要加
# 4 string (with pointer)
## 4.1 三大函数：拷贝构造、拷贝赋值、析构函数
```cpp
class String
{
public:          //不能用编译器自带的拷贝构造、拷贝赋值
    String(const char* cstr = 0);   //构造函数
    String(const String& str);    //拷贝构造，接受的是自己的对象
    String& operator=(const String& s);   //拷贝赋值，接受的是自己的对象
    ~String();   //析构函数，这个类的对象死亡的时候调用
    char* get_c_str() const { return m_data};  //inline（成员函数）
private:
    char* m_data;  //字符串里面存放一个指针，在需要内存的时候创建另外一个空间来放字符
};
```
### 4.1.1 构造函数、析构函数
```cpp
inline 
String::String(const char* cstr = 0)   //构造函数
{
    if(cstr)
    {
        m_data = new char[strlen(cstr)+1];   //传进来的字符串长度加结束符
        strcpy(m_data, cstr);
    }
    else
    {//未指定初值,空指针
        m_data = new char[1];     //new 动态分配一块内存
        *m_data = '\0';    //空指针仍要分配一个内存存放结束符号
    }
}

inline 
String::~String()    //析构函数
{
    delete[] m_data;   //释放掉动态分配的内存
}

{
    String s1();       //调用构造函数，在作用域结束时自动调用析构函数
    String s2("hello");   

    String* p = new String("hello");  //动态的创建对象
    delete p;  //手动释放内存
}
```
### 4.1.2 拷贝构造、拷贝赋值
```带有指针的class，必须有拷贝构造、拷贝赋值```
#### 拷贝构造 

<img src="https://img-blog.csdnimg.cn/9a48fb2d0da0429994017b236040b23e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="60%" alt="还在路上，稍等..."/>

编译器默认的拷贝构造、拷贝赋值是浅拷贝，只是拷贝对象里值，这里只复制了指针过去，两个对象指向同一个字符串，并且会造成内存泄漏。
```cpp
inline 
String::String(const String& str)    //拷贝构造
{
    m_data = new char[strlen(str.m_data)+1];   //分配内存
    strcpy(m_data, str.m_data);      //把内容拷贝过去   深拷贝
}                     //直接取另一个对象的private data，同一个类的对象互为友元

{
    String s1("hello");
    String s2(s1);   //拷贝构造
//  String s2 = s1;  
}
```
#### 拷贝赋值
```cpp
inline 
String& String::operator=(const String&) 
{
    if(this == &str)//检测自我赋值，不只是为了效率，防止杀掉自己而丢失内存的控制
        return *this;   
    
    delete[] m_data;              //1.杀掉自己
    m_data = new char[strlen(str.m_data) + 1]; //2.重新分配内存
    strcpy(m_data, str.m_data);   //3.拷贝内容
    return *this;  
}
```
```cpp
#include <iostream.h>
ostream& operator<<(ostream& os, const String& str)   //output重载  只能是全局函数
{
    os << str.get_c_str();   //直接把指针给cout
    return os;
}
```
## 4.2 stack（栈），heap（堆）
**Stack**，是存在于某```作用域```的一块内存空间。例如当你调用函数，函数本身即会形成一个stack用来放置它所接收的参数，以及返回地址。
在```函数本体内声明```的任何变量，其所使用的内存块都取自上述stack。
**Heap**，是指操作系统提供的一块```全局```内存空间，程序可动态分配（new）。
```cpp
class Complex{...};
...
{
    Complex c1(1, 2);    //内存来自tack
    Complex* p = new Complex(3);   //内存来自heap，需要手动delete
}   //离开作用域时c1死亡
```
```cpp
class Complex{...};
...
Complex c3(1,2);
{
    Complex c1(1, 2);
    static Complex c2(1, 2);
}
```
c1是```stack object```，其生命在作用域结束时也结束了，这种作用域内的object，又称为auto object，因为它会被自动清理（自动调用析构函数）。	
c2是```static object```，其生命在作用域结束之后仍然存在，知道整个程序结束。
c3是```global object```，其生命在整个程序结束之后结束。也可以把他视为一种static object，其作用域是整个程序。
 **heap object的生命周期**
```cpp
class Complex{...};
...
{
    Complex* p = new Complex;
    ...
    delete p;
}
```
p所指的便是heap object，其生命在它被delete时结束。
如果没有```delete```，在作用域结束时p所指的heap object仍然存在，但指针p的声明结束了，造成内存泄漏。
**new:先分配内存，再调用构造函数**
```cpp
Complex* pc = new Complex(1, 2);
//new被分解为三个步骤
Complex *pc;
void* mem = operator new(sizeof(Complex));//分配内存
pc = static_cast<Complex*>(mem);//转型
pc->Complex::Complex(1, 2);//构造函数
```

<img src="https://img-blog.csdnimg.cn/dc196757a51d4924ba9c9124806db62e.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="80%" alt="还在路上，稍等..."/>

**delete：先调用析构函数，再释放内存**
<img src="https://img-blog.csdnimg.cn/f1b488aecf604d3fb53e637032353af1.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="80%" alt="还在路上，稍等..."/>
## 4.3 动态分配所得的内存块，in VC
### ```new```一个```complex```、```string```所得到的内存：
<img src="https://img-blog.csdnimg.cn/b4b360f0179e4b0a9718bb6de08f4f6f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="60%" alt="还在路上，稍等..."/>

- **绿色**：类的对象
- **灰色**：调试模式下上面32，下面4。release模式下没有灰色模块
- **紫色**：cookie，上下各4个字节，用来记录整块内存的大小，方便回收。cookie的值是内存块大小的16进制，因为是16的倍数最低位是0，用最低位为1来表示内存块被分配出去。
- **绿色**（pad）：在VC里所给的每一个内存块都是16的倍数，不够需要填补

### new一个```array```所得到的内存
<img src="https://img-blog.csdnimg.cn/f09f1910fbee4d588636f2f03c29e444.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="60%" alt="还在路上，稍等..."/>

这里多四个字节，用一个整数来记录数组的大小
```array new```要搭配```array delete```。
<img src="https://img-blog.csdnimg.cn/1e38e86e465c4d8d85359d6c89d0c5b5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="60%" >
如果```delete```没有加```[]```，如果是不带指针的类，对象会被回收，但带指针的类的对象里的指针所指的内存只有第一个被回收，而造成内存泄漏。
## 4.3 static
<img src="https://img-blog.csdnimg.cn/162d668a69c941cfa019fe84ea915e75.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="90%" >

### 4.3.1 this point
只要在数据或函数前面加上```static```，它就成为```静态数据```或```静态函数```。
```cpp
complex c1,c2,c3;
c1.real();  ——>  complex::real(&c1);
```
谁调用，谁就是```this point```,c1调用，c1的地址就是this point。调用相同的函数，传给它的是不同的地址，才能处理不同的数据，这个地址是this point。
```cpp
class complex
{
public:
	double real () const
		{ return this->re; }
private:
	double re, im;
}
```
### 4.3.2 成员函数与静态函数的区别：
- ```成员函数```有一个隐藏的```this point```，不能写进参数，可以在函数里使用，函数里的this可写可不写，不写编译器会自动加上。 	
- ```静态函数```没有```this point```,所以不能通过```this```指针来访问各个对象，只能处理静态数据。
### 4.3.3 调用static函数
```cpp
class Account
{
public:
    static double m_rate;                            //静态数据   声明
    static void set_rate(const double& x){m_rate = x;}    //静态函数
};
double Account::m_rate = 8.0; 

int main()
{
    Account::set_rate(5.0);

    Account a;
    a.set_rate(7.0);
}
```
如果是```静态数据```，一定要在class外加上:
```cpp
double Account::m_data = 8.0;  //定义   有没有初值都可以
```
使变量获得内存的操作叫```定义```。
```调用static函数```的方式：
- 通过object调用
- 通过class name调用
### 4.3.4 补充singleton
```cpp
class A
{
public:
    static A& getInstance{return a;};  //取得唯一的对象
    setup(){...}
private:
    A();     //任何人不能创建
    A(const A& rhs);
    static A a;   //创建一个对象
    ...
};

A::getInstance().setup();
```
如果没有人调用这个函数，静态的a仍然存在
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
    static A a;   //使用单例的时候才会创建
    return a;
}
```
### 4.4 cout
```cpp
class _IO_ostream_withassign:public ostream{
    ...
};
extern _IO_ostream_withassign cout;

class ostream:virtual public ios
{
public:
    ostream& operator<<(char c);
    ostream& operator<<(unsigned char c){return (*this)<<(char)c;}
    ostream& operator<<(signed char c){return (*this)<<(char)c;}
    ostream& operator<<(const char *s);
    ostream& operator<<(const unsigned char *s)
    {return (*this) << (const char*)s;}
    ostream& operator<<(const signed char *s)
    {reutrn (*this) << (const char*)s;}
    ostream& operator<<(const void *p);
    ostream& operator<<(int n);
    ostream& operator<<(unsigned int n);
    ostream& operator<<(long n);
    ostream& operator<<(unsigned long n);
    ...
};
```
```cout```对每个类型都做了重载，才能打印出各种数据。
### 4.5 函数模板，function template
```cpp
stone r1(2,3),r(3,3),r3;
r3 = min(r1, r2);  //编译器会对function template进行实参推导，因此不必像class template指出类的名称

template<class T>   //class和typename是相通的
inline const T& min(const T& a, const T& b)
{
    return b < a ? b : a; //推导出T为stone 调用操作符重载 stone::operator<
                          //函数模板不用管怎么比大小，是由类的内容决定的
}
```
### 4.6 补充namespace
```cpp
namespace std
{
    ...
}
```
标准库所有东西都被包装在```std```中。
调用方式：
- using namespace std；
- using std::cin；
- std::cin
# 5 继承、复合、委托
## 5.1 Composition(复合)
### 5.1.1 复合，表示has-a
```cpp
template <class T, class Sequence = deque<T>>
class queue
{
    ...
protected:
    Sequence c;   //底层容器
public:
    //以下完全利用c的操作函数完成
    bool empty() const {return c.empty();}
    size_type size() const {return c.size();}
    reference front() {return c.front();}
    reference back() {return c.back();}
    //deque是两端可进出，queue是末端进前端出（先进先出）
    void push(const value_type& x) {c.push_back(x);}
    void pop() {c.pop_front();}
};
```
**把```deque<T>```替换进去**
<img src="https://img-blog.csdnimg.cn/596eb4fa4a5e440db1b53619c80bbe41.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="80%" >
class queue里面有deque<T>,has-a的关系。
黑色菱形表示```有```，queue拥有了、容纳了deque这个类
```Adapter设计模式```：queue拿deque的部分功能改装为一个新的class
### 5.1.2 从内存来看composition的关系
<img src="https://img-blog.csdnimg.cn/bb1b8cbc3532430a9741deae35896747.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="80%" >

内存上是包含的关系
### 5.1.3 复合关系下的构造和析构
<img src="https://img-blog.csdnimg.cn/2b1c935e2646401b9a45f48b1e50d2fd.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="60%" >

- 构造由内而外
 ```container```的构造函数首先调用```component```的default构造函数，然后才执行自己。
- 析构由外而内
```container```的析构函数首先执行自己，然后才调用```component```的析构函数。
## 5.2 Delegation(委托). Composition by reference
<img src="https://img-blog.csdnimg.cn/43773a8fabe64b399d9933dda4d5336f.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="60%" >

左边有一个```指针```指向右边，不是完全包含的关系，两边寿命不一致。
**```pimpl```(handle/body)编译防火墙：**
左边只是对外的接口，真正的实现都在右边做，左边调用右边类的函数。右边类的变动不会影响左边。
a、b、c共享一份内存。当a响要改变数组“hello”时复制一份给它。copy on right
## 5.3 Inheritance(继承)
### 5.3.1 表示is-a
<img src="https://img-blog.csdnimg.cn/ba671206cb6e49049c0591e8d78c1448.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_15,color_FFFFFF,t_70,g_se,x_16" width="30%" >

```cpp
struct _List_node_base
{
    _List_node_base* _M_next;
    _List_node_base* _M_prev;
};

template<typename _Tp>
struct _List_node:public _List_node_base
	:public _List_node_base    //公共继承语法  共有三种继承
{
    _Tp _M_data;
};
```
父类的数据时可以完整的继承下来
### 5.3.2 继承关系下的构造函数和析构函数
<img src="https://img-blog.csdnimg.cn/99778646328249758ec89d69fdbd28a5.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="78%" >

## 5.4 Inheritance（继承）with virtual function（虚函数）
**语法**：只要在任何一个成员函数之前加上virtual，它就成为虚函数
子类继承父类```所有的数据```，和```函数的调用权```。父类的函数子类全部可以调用，但是子类要不要重新定义：
**从虚函数角度将成员函数分为三种:**
- non-virtual 非虚函数：不希望子类重新定义(override，覆写)
- virtual 虚函数：希望子类重新定义它，且对它已有默认定义。
- pure virtual 纯虚函数：希望子类一定要重新定义它，你对它没有默认定义。（可以有定义）
<img src="https://img-blog.csdnimg.cn/9bad35ff36224adb91ba0cef4c10aef2.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="78%" >

**template method**
<img src="https://img-blog.csdnimg.cn/c48b60a855d94ef78e8a4e1195367788.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="90%" >
## 5.5 继承+复合关系下的构造和析构
<img src="https://img-blog.csdnimg.cn/86d54f98f25c46dcbc7bb7d5612cf7c4.png?x-oss-process=image/watermark,type_ZHJvaWRzYW5zZmFsbGJhY2s,shadow_50,text_Q1NETiBAQ3lZdV8=,size_20,color_FFFFFF,t_70,g_se,x_16" width="60%" >
## 5.6 委托+继承


























































