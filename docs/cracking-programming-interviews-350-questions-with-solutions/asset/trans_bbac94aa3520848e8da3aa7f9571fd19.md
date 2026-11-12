
## 并发安全的位域

如果两个位域位于不同的内存位置，则两个线程并发更新它们是安全的

- *bitfield_b* 和 *bitfield_c* 位于同一内存位置，因此并发更新不是线程安全的。
- *bitfield_c* 和 *bitfield_d* 位于不同的内存位置，因为它们被一个零长度位域分隔，因此并发更新是线程安全的。
- *bitfield_d* 和 *bitfield_a1* 位于不同的内存位置，因为 *bitfield_a1* 位于嵌套结构 E 内，因此并发更新是线程安全的。
- *bitfield_f* 和 *bitfield_h* 位于不同的内存位置，因为它们被一个*非位域*数据成员 *non_bitfield_g* 分隔，因此并发更新是线程安全的。

因此，如果同一结构体中两个位域之间的所有字段也都是非零宽度的位域，那么并发更新这两个位域是不安全的，因为它们构成同一内存位置。

与结构体 A 相关联的内存位置有七个

- 1. *non_bitfield_a*
- 2. *bitfield_b* 和 *bitfield_c*
- 3. *bitfield_d*
- 4. *bitfield_a1* (*non_bitfield_e*)
- 5. *bitfield_f*
- 6. non_bitfield_g
- 7. bitfield_h

```c
struct A
{
    char non_bitfield_a;
    int bitfield_b    : 3;
    int bitfield_c    : 10;
    int               : 0;

    int bitfield_d    : 8;

    struct E
    {
        int bitfield_a1 : 8;
    } non_bitfield_e;

    int bitfield_f    : 4;
    int non_bitfield_g;
    int bitfield_h    : 11;
};
```

## 问题 2 不同的地址位置

下面程序编译时会发生什么？

程序 8.3：不同的地址位置

```cpp
int main()
{
    char a = 'a';
    char b = 'b';
    static_assert(&a == &b, "Address_of_a_and_b_"
                          "should_be_distinct");
}
```

### 问题 2 的解答

它会导致如下所列的编译错误：

```text
distinct_add.cpp: In function 'int main()':
distinct_add.cpp:6:6:
error: static assertion failed:
Address of a and b should be distinct
     static_assert(&a == &b, "Address of a and b "
     ^
```

两个不同对象的地址位置总是不同的，除非以下情况为真，此时结果由实现定义：

- 1. 它们是位域
- 2. 它们是零大小的基类子对象

对象的地址是其占用的第一个字节的地址，除非它是位域或零大小的基类子对象。

## 问题 3 信号和值

列出即使在发生信号时其值也保证有定义的对象类型？

### 问题 3 的解答

- 1. volatile std::sig_atomic_t
- 2. 无锁原子对象

## 问题 4 临时对象和转换

在下面程序中，第 12 行的临时对象被销毁之前会发生什么？

程序 8.4：临时对象和转换

```cpp
struct A
{
    A(int x) : _x(x) {}

    int & val() { return _x; }
private:
    int _x;
};

int main()
{
    if(A(1).val())
    {}
}
```

### 问题 4 的解答

在类型 A 的临时对象销毁之前，会发生以下转换

- 1. 左值到右值转换
- 2. int 到 bool 转换

## 问题 5 表达式的求值

请查看下面的程序：

程序 8.5：表达式的求值

```cpp
void compute(int, int) {}
void eval(int x, int arr[])
{
    x = arr[x++];

    x = 2, x++, x++;

    x = x++ + 1;
    x = x + 1;

    compute(x = -1, x = -1);
}
```

### 问题 5 的解答

- 第 5 行：行为未定义
- 第 7 行：x 变为 4
- 第 9 行：行为未定义
- 第 10 行：x 的值递增
- 第 12 行：行为未定义

## 问题 6 三字符序列

这里的三字符序列会发生什么：

```
Program 8.6: trigraph sequences
1??=define validateArray(x, y) x??(y??) ??!??! y??(x??)
```

### 问题 6 的解答

- 三字符序列 ??= 被替换为 #
- 三字符序列 ??( 被替换为 [
- 三字符序列 ??) 被替换为 ]
- 三字符序列 ??! 被替换为 |

上述情况 ⇒ 所述三字符序列将被替换，使表达式变为如下形式

```
Program 8.7: replacing trigraph sequences
1#define validateArray(x, y) x[y] || y[x]
```

## 问题 7 自增运算符

该程序的输出是什么：

```
Program 8.8: increment operator
1#include <iostream>
2
3int main()
4{
5    int one = 1;
6    int two = 2;
7
8    int a = one+++++two;
9 }
```

### 问题 7 的解答

编译时，错误为：

```text
increment_operator.cpp: In function ‘int main()’:
increment_operator.cpp:8:18:
error: lvalue required as increment operand
    int a = one+++++two;
```

表达式 `one+++++two` 被解析为类似 `one ++ ++ + two` 的形式，这违反了自增运算符的约束，从而导致表达式不正确。

*one+++++two ⇒ one ++ ++ + two*

请注意，表达式 `one+++++two` 不会被解析为 `one ++ + ++ two`，后者确实是一个正确的表达式。

*one+++++two ⇒ one ++ ++ + two*

## 问题 8 — nullptr

`nullptr` 是什么？

### 问题 8 的解答

`nullptr` 是指针字面量，表示类型为 `std::nullptr_t` 的纯右值。它是一个空指针常量，可以转换为空指针值或空成员指针值。

请注意，`std::nullptr_t` 本身

- 不是指针类型
- 不是成员指针类型
- 是一种不同的类型

## 问题 9 — 用户定义字面量

*用户定义字面量*是什么？

### 问题 9 的解答

*用户定义字面量* 是对以下形式的字面量运算符或字面量运算符模板的调用

- 1. `operator "" identifier`
- 2. `operator "" identifier<'c₁', 'c₂', ..., 'cₖ'>()`

例如：

- 1. `user-defined-integer-literal`
  - a) `operator "" identifier (n ULL)`
  - b) `operator "" identifier ("n")`
  - c) `operator "" identifier <'c1', 'c2', ... 'ck'>()`
- 2. *user-defined-floating-literal*
  - a) `operator "" identifier (f L)`
  - b) `operator "" identifier ("ff")`
  - c) `operator "" identifier <'c1', 'c2', ... 'ck'>()`
- 3. *user-defined-string-literal*
  - a) `operator "" identifier (str, len)`
  - b) `operator "" identifier (ch)`
  - c) `operator "" identifier <'c1', 'c2', ... 'ck'>()`

程序 8.9：用户定义字面量

```cpp
#include <string>

void operator "" _distance(long double);
long double operator "" _amount(long double);

std::string operator "" _amount(const char16_t *,
                                std::size_t);

unsigned operator "" _amount(const char*);
float operator "" _X(const char*);

template <char...> int operator "" _length();

int main()
{
    2.9_amount;

    u"test"_amount;

    20_amount;
}
```

在上面的示例中

- 第 18 行调用 operator "" _amount(2.9L)
- 第 20 行调用 operator "" _amount(u"test", 4)
- 第 22 行调用 operator "" _amount("20")

## 问题 10 声明与定义

以下哪些是定义，哪些只是声明？

程序 8.10：声明与定义

```cpp
1 extern int a1;
2 int a2;
3 extern const int a3;
4 extern const int a4 = 10;
5 void fun(int);
6 void fun(int) {}
7 struct A;
8 struct A
9 {
10     int x, y;
11 };
12 typedef int Integer;
13 enum { low, mid, high };
14 extern A _A;
15 struct B
16 {
17     static int x;
18 };
19 int B::x = 5;
20 namespace Detail { int x; }
21 using Detail::x;
22 namespace DetailsX = Detail;
23 B b1;
```

### 问题 10 的解答

- *声明*  
  第 1、3、5、7、12、14、17、21 行
- *定义*  
  其余为定义

## 问题 11 — 编译器生成的成员函数

在以下情形中，列出其定义由编译器隐式生成的成员函数：

程序 8.11：示例类

```cpp
1 #include <string>
2 struct A
3 {
4     std::string __str;
5 };
6 
7 int main()
8 {
9     A a1;
10    A a2 = a1;
11    a2 = a1;
12 }
```
