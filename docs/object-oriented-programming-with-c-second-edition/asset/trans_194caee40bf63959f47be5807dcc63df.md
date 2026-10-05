

# 使用 C++ 进行面向对象编程

print(print(print(cout,s1),s2),s3);

然而，语句

cout<<s1<<s2<<s3;

此外，在模板的情况下会发生什么呢？让我们考虑一个常见的全局模板函数，它调用了嵌入内部的插入运算符。如果我们想通过传递一个 `String` 类对象作为参数来使用此类函数，插入运算符将自动传递到该对象上。如果 `String` 类没有重载插入运算符，则会导致编译时错误。模板的章节（第 10 章）中关于函数模板的叙述和示例阐明了这一点。提取运算符重载的原因与插入运算符类似。`String::setString()` 函数的问题在于，客户端需要先将它 想要存储在 `String` 类对象中的字符串加载到缓冲区中，然后将其传递给该函数。该函数的形参数类型与存储字符串的成员变量类型相同。显然，缓冲区也应该是相同类型。该函数的问题是，缓冲区必须传递给函数，并且该数组的类型必须与存储它的成员变量类型相同。如果类型发生变化，缓冲区的类型也需要发生变化。这迫使客户端进行更改。但是，如果为 `String` 类重载了提取运算符，可以使用以下语句代替调用 `String::setString()` 函数：

```cpp
cout<<s1;
```

读取数据的责任被转移到了对象本身。数据在对象中的存储方式以及其中的任何更改都将不再影响客户端。

重载插入和提取运算符是为了实现实现（成员函数定义）与接口（成员函数原型）的分离。

## 8.2.7 重载 new 和 delete 运算符

`new` 和 `delete` 运算符可以针对特定类进行重载。这些运算符的行为可以通过特定类的的操作数来改变。

如果这些运算符针对特定类进行了重载，那么当类类型作为参数传递给这些运算符时，就会调用重载它们的函数。否则，将重载全局的 `new` 和 `delete` 运算符。例如，如果 `new` 运算符已经为类 X 重载过，但没有为类 Y 重载过，那么语句

```cpp
* Xptr = new X;
```

将调用重载了类 X 的 `new` 运算符的函数。但语句

```cpp
* Yptr = new Y;
```

将调用全局运算符。有趣的是，如果将重载 `new` 和 `delete` 运算符的函数插入类中或从类中移除，用户程序可能不会改变。

重载 `new` 运算符（为单个对象分配内存）的语法如列表 8.39 所示。

## 运算符重载、类型转换、新风格转换以及 RTTI

**列表 8.39** 重载 `new` 运算符并为单个对象分配内存的语法

```cpp
class <class_name>
public:
    static void * operator new(size_t); //函数
    /*
    //原型
    类的其余部分
    */
};
void <class_name> :: operator new ( size_t size )
    //函数定义
{
    /*
    函数的定义
    */
}
```

重载 `new` 运算符（为对象数组分配内存）的语法在列表 8.40 中。

**列表 8.40** 重载 `new` 运算符并为对象数组分配内存的语法

```cpp
class <class_name>
public:
    static void * operator new [](size_t); //函数
    /*
    //原型
    类的其余部分
    */
};
void <class_name>::operator new [] ( size_t size )
    //函数定义
{
    /*
    函数的定义
    */
}
```

重载 `delete` 运算符（释放单个对象的内存）的语法在列表 8.41 中。

**列表 8.41** 重载 `delete` 运算符并释放单个对象内存的语法

```cpp
class <class_name>
public:
    static void operator delete(void *,size_t);
    //函数原型
    /*
/* 类的其余部分
 */
void <class_name>::operator delete (void * p, size_t size)
    //函数定义
```

```cpp
/*
函数的定义
*/
```

重载 `delete` 运算符（释放对象数组的内存）的语法在列表 8.42 中。

列表 8.42 重载 `delete` 运算符并释放对象数组内存的语法

```cpp
class <class_name>
    public:
        static void operator delete [] (void *, size_t);
        //函数原型
        /*
        类的其余部分
        */
```

```cpp
/*
函数的定义
*/
void <class_name>::operator delete []void *, size_t size)
    //函数定义
```

`operator new` 函数和 `delete` 运算符函数必须是静态的。然而，它们的原型可以不带有 `static` 关键字。无论如何，编译器都会将这些函数视为静态的（原因在本章中解释）。

`operator new` 函数的返回类型必须是 `void *` 类型。该函数返回的值是通过调用全局 `new` 运算符得到的内存块地址。`operator new` 函数至少应该接收一个 `size_t` 类型的形参数。`size_t` 参数处理要分配的内存量。

