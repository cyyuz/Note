# C++11

## 可变参数模板



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

## lambda

lambda 是一个闭名的 function object，作用是一个 (inline) function。

### 匿名函数语法
```[capture] (parameters) mutable ->return-type{statement} ```

- `[capture]`：捕捉列表。`[]` 表示 lambda 函数，捕捉列表能捕捉上下文中的变量供 lambda 函数使用。在块作用域以外的lambda捕捉列表必须为空。
- `(parameeters)`：参数列表。如果没有参数，可以省略`()`。
- `mutable`：默认 lambda 函数是 const 函数，mutable 可以取消常量性。使用时，参数列表不能省略。
- `->return-type`：返回类型。没有返回值时可以省略，或返回类型明确时，编译器对返回类型进行推导。
- `{statement}`：函数体。除了可以使用参数，还能使用捕获的变量。

> 可以忽略`参数列表`和`返回类型`，但不可以忽略```捕获列表```和```函数体```

**lambda 函数与普通函数的最大区别**之一，就是 lambda 可以通过捕捉列表访问一些上下文中的数据。

|语法 |描述|
|-|-|
|[var]|表示值传递方式捕捉变量var。在 lambda 函数中是不可更改的常量。|
|[=]|表示值传递方式捕捉所有父作用域的变量，包括this。pass by value|
|[&var]|表示引用传递捕捉变量var。|
|[&]| 表示引用传递捕捉所有父作用域的变量，包括this。pass by reference |
|[this]|表示值传递方式捕捉当前的this指针。|

### lambda和仿函数

仿函数是编译器实现 lambda 的一种方式，通常编译器都会把 lambda 函数转化为成为一个仿函数对象。

```c++
int id = 0;
auto f = [id]() mutable {
	std::cout << "id:" << id << std::endl;
	++id;
}

id = 42;
f();
f();
f();
std::cout << id << std::endl;   // 0 1 2 42
```

```c++
class Functor {
private:
    int id;
public:
	void operator()(){  // operator()被重载
        std::cout << "id:" << id << std::endl;
		++id;
    }  
};
Functor f;
```

**lambda 和仿函数**都可以捕捉一些变量作为初始状态并接受参数进行运算。lambda 函数捕捉了作用域数据，而仿函数则以作用域数据初始化类。lambda 捕捉的变量都会成为等价仿函数的成员变量，而常量成员函数(如operator())中改变其值是不允许的。

使用 lambda 代替仿函数的应该满足如下一些条件:

- 局限于一个局部作用城中使用的代码逻辑。
- 这些代码逻辑需要被作为参数传递。

lambda 函数并非函数指针，C++11 允许 lambda 表达式向函数指针的转换，前提是 lambda 函数没有捕捉任何变量，且函数指针所指的函数原型，必须跟 lambda 函数有着相同的调用方式。

## inline

如果函数在```class body```内定义，自动成为```inline候选```，如果在 class 本体外定义就不是 inline。
inline 只是对编译器的建议，由编译器决定，如果函数太复杂，编译器就没有能力把函数变成 inline。

```cpp     
inline double  //如果在body外定义,可以在前面加上inline 
imag(const complex& x)
{
    return x.imag ();
}
```

## std::function和bind

## 委托构造和继承构造



## 移动构造和





# C++14



# C++17

fold expression
