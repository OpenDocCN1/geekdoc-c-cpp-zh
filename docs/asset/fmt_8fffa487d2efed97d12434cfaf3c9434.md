
```
1  // Fig. 22.14: fig22_14.cpp
2  // Using virtual base classes.
3  #include <iostream>
4  using std::cout;
5  using std::endl;
6
```

Fig. 22.14 | Using virtual base classes. (Part 1 of 3.)

```
7  // class Base definition
8  class Base
9  {
10 public:
11     virtual void print() const = 0; // pure virtual
12 }; // end class Base
13
14 // class DerivedOne definition
15 class DerivedOne : virtual public Base
16 {
17 public:
18     // override print function
19     void print() const
20     {
21         cout << "DerivedOne\n";
22     } // end function print
23 }; // end DerivedOne class
24
25 // class DerivedTwo definition
26 class DerivedTwo : virtual public Base
27 {
28 public:
29     // override print function
30     void print() const
31     {
32         cout << "DerivedTwo\n";
33     } // end function print
34 }; // end DerivedTwo class
35
36 // class Multiple definition
37 class Multiple : public DerivedOne, public DerivedTwo
38 {
39 public:
40     // qualify which version of function print
41     void print() const
42     {
43         DerivedTwo::print();
44     } // end function print
45 }; // end Multiple class
46
47 int main()
48 {
49     Multiple both; // instantiate Multiple object
50     DerivedOne one; // instantiate DerivedOne object
51     DerivedTwo two; // instantiate DerivedTwo object
52
53     // declare array of base-class pointers and initialize
54     // each element to a derived-class type
55     Base *array[ 3 ];
56     array[ 0 ] = &both;
57     array[ 1 ] = &one;
58     array[ 2 ] = &two;
59
```

```
```cpp

// polymorphically invoke function print

for ( int i = 0; i < 3; i++ )

    array[ i ]->print();

return 0;

} // end main

```
```

DerivedTwo

DerivedOne

DerivedTwo

**Fig. 22.14** | Using virtual base classes. (Part 3 of 3.)

## Constructors in Multiple-Inheritance Hierarchies with virtual Base Classes

Implementing hierarchies with virtual base classes is simpler if default constructors are used for the base classes. The examples in Figs. 22.13 and 22.14 use compiler-generated default constructors. If a virtual base class provides a constructor that requires arguments, the implementation of the derived classes becomes more complicated, because the *most derived class* must explicitly invoke the virtual base class’s constructor to initialize the members inherited from the virtual base class.

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_933_0.png)

> **Software Engineering Observation 22.5**
>
> > Providing a default constructor for virtual base classes simplifies hierarchy design.

## Additional Information on Multiple Inheritance

Multiple inheritance is a complex topic typically covered in more advanced C++ texts. For more information on multiple inheritance, please visit our C++ Resource Center at

`www.deitel.com/cplusplus/`

In the C++ *Multiple Inheritance* category, you’ll find links to several articles and resources, including a multiple inheritance FAQ and tips for using multiple inheritance.

## 22.9 Wrap-Up

In this chapter, you learned how to use the `const_cast` operator to remove the const qualification of a variable. We then showed how to use namespaces to ensure that every identifier in a program has a unique name and explained how they can help resolve naming conflicts. You saw several operator keywords for programmers whose keyboards do not support certain characters used in operator symbols, such as `!`, `&`, `^`, `~` and `|`. Next, we showed how the `mutable` storage-class specifier enables a programmer to indicate that a data member should always be modifiable, even when it appears in an object that is currently being treated as a const. We also showed the mechanics of using pointers to class members and the `->*` and `.*` operators. Finally, we introduced multiple inheritance and discussed problems associated with allowing a derived class to inherit the members of several base classes. As part of this discussion, we demonstrated how virtual inheritance can be used to solve those problems.

## 运算符优先级与结合性表

### A.1 运算符优先级

运算符按优先级从高到低自上而下排列（图 A.1）。

| 运算符 | 类型 | 结合性 |
|---|---|---|
| :: | 二元作用域解析 | 从左到右 |
| :: | 一元作用域解析 | 从左到右 |
| () | 圆括号 | 从左到右 |
| [] | 数组下标 | 从左到右 |
| . | 通过对象选择成员 | 从左到右 |
| -> | 通过指针选择成员 | 从左到右 |
| ++ | 一元后缀自增 | 从左到右 |
| -- | 一元后缀自减 | 从左到右 |
| typeid | 运行时类型信息 | 从左到右 |
| dynamic_cast < type > | 运行时类型检查转换 | 从左到右 |
| static_cast< type > | 编译时类型检查转换 | 从左到右 |
| reinterpret_cast< type > | 用于非标准转换的强制转换 | 从左到右 |
| const_cast< type > | 去除 const 属性的转换 | 从左到右 |
| ++ | 一元前缀自增 | 从右到左 |
| -- | 一元前缀自减 | 从右到左 |
| + | 一元正号 | 从右到左 |
| - | 一元负号 | 从右到左 |
| ! | 一元逻辑非 | 从右到左 |
| ~ | 一元按位取反 | 从右到左 |
| sizeof | 确定字节大小 | 从右到左 |
| & | 取地址 | 从右到左 |
| * | 解引用 | 从右到左 |
| new | 动态内存分配 | 从右到左 |
| new[] | 动态数组分配 | 从右到左 |
| delete | 动态内存释放 | 从右到左 |
| delete[] | 动态数组释放 | 从右到左 |
| ( type ) | C 风格一元强制转换 | 从右到左 |
| .* | 指向成员的指针（通过对象） | 从左到右 |
| ->* | 指向成员的指针（通过指针） | 从左到右 |
| * | 乘法 | 从左到右 |
| / | 除法 | 从左到右 |
| % | 取模 | 从左到右 |
| + | 加法 | 从左到右 |
| - | 减法 | 从左到右 |
| << | 按位左移 | 从左到右 |
| >> | 按位右移 | 从左到右 |
| < | 关系运算：小于 | 从左到右 |
| <= | 关系运算：小于或等于 | 从左到右 |
| > | 关系运算：大于 | 从左到右 |
| >= | 关系运算：大于或等于 | 从左到右 |
| == | 关系运算：等于 | 从左到右 |
| != | 关系运算：不等于 | 从左到右 |
| & | 按位与 | 从左到右 |
| ^ | 按位异或 | 从左到右 |
| \| | 按位或 | 从左到右 |
| && | 逻辑与 | 从左到右 |
| \|\| | 逻辑或 | 从左到右 |
| ?: | 三元条件运算符 | 从右到左 |
| = | 赋值 | 从右到左 |
| += | 加赋值 | 从右到左 |
| -= | 减赋值 | 从右到左 |
| *= | 乘赋值 | 从右到左 |
| /= | 除赋值 | 从右到左 |
| %= | 取模赋值 | 从右到左 |
| &= | 按位与赋值 | 从右到左 |
| ^= | 按位异或赋值 | 从右到左 |
| \|= | 按位或赋值 | 从右到左 |
| <<= | 按位左移赋值 | 从右到左 |
| >>= | 按位右移赋值 | 从右到左 |
| , | 逗号 | 从左到右 |

图 A.1 | 运算符优先级与结合性表。

## ASCII 字符集

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| 0 | nul | soh | stx | etx | eot | enq | ack | bel | bs | ht |
| 1 | lf | vt | ff | cr | so | si | dle | dc1 | dc2 | dc3 |
| 2 | dc4 | nak | syn | etb | can | em | sub | esc | fs | gs |
| 3 | rs | us | sp | ! | " | # | $ | % | & | ' |
| 4 | ( | ) | * | + | , | - | . | / | 0 | 1 |
| 5 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | : | ; |
| 6 | < | = | > | ? | @ | A | B | C | D | E |
| 7 | F | G | H | I | J | K | L | M | N | O |
| 8 | P | Q | R | S | T | U | V | W | X | Y |
| 9 | Z | [ | \\ | ] | ^ | _ | \` | a | b | c |
| 10 | d | e | f | g | h | i | j | k | l | m |
| 11 | n | o | p | q | r | s | t | u | v | w |
| 12 | x | y | z | { | \| | } | ~ | del |  |  |

图 B.1 | ASCII 字符集。

表格左侧的数字是字符代码的十进制等效值（0–127）的左位数字，表格顶部的数字是字符代码的右位数字。例如，“F”的字符代码是 70，“&”的字符代码是 38。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_938_0.png)

## 基本类型

图 C.1 列出了 C++ 的基本类型。C++ 标准文档没有给出在内存中存储这些类型变量所需的确切字节数。但是，C++ 标准文档确实指出了基本类型内存需求之间的关系。按内存需求从小到大的顺序，浮点类型为 `float`、`double` 和 `long double`。与整数类型一样，`double` 的存储空间必须至少与 `float` 一样大，`long double` 的存储空间必须至少与 `double` 一样大。

| 整型 | 浮点型 |
|---|---|
| bool | float |
| char | double |
| signed char | long double |
| unsigned char |  |
| short int |  |
| unsigned short int |  |
| int |  |
| unsigned int |  |
| long int |  |
| unsigned long int |  |
| wchar_t |  |

**图 C.1** | C++ 基本类型。

基本类型的确切大小和取值范围由实现决定。头文件 `<climits>`（用于整型）和 `<cfloat>`（用于浮点型）指定了系统支持的值范围。

类型支持的值范围取决于用于表示该类型所使用的字节数。例如，假设一个系统的 `int` 为 4 字节（32 位）。对于有符号 `int` 类型，非负值范围为 0 到 2,147,483,647（2³¹ − 1）。负值范围为 −1 到 −2,147,483,648（−2³¹）。总共 2³² 个可能值。同一系统上的无符号 `int` 将使用相同的位数来表示数据，但不表示任何负值。因此其值范围为 0 到 4,294,967,295（2³² − 1）。在同一系统上，`short int` 表示数据所用的位数不能超过 32 位，而 `long int` 必须至少使用 32 位。

C++ 提供 `bool` 数据类型，用于只能保存 `true` 和 `false` 这两个值的变量。

## D 预处理器

### 目标

在本附录中，你将学习：

- 使用 `#include` 开发大型程序。
- 使用 `#define` 创建宏和带参数的宏。
- 理解条件编译。
- 在条件编译期间显示错误消息。
- 使用断言测试表达式的值是否正确。

> 坚守善，并善加定义。
> ——阿尔弗雷德·丁尼生勋爵
> 我已为你找到了一个论点；但我没有义务让你理解。
> ——塞缪尔·约翰逊
> 一个好的符号是最好的论据，也是说服千千万万人的传教士。
> ——拉尔夫·沃尔多·爱默生
> 条件从根本上是健全的。
> ——赫伯特·胡佛 [1929年12月]
> 党徒在争论时，毫不在意问题的对错，只急于让听众相信他自己的主张。
> ——柏拉图

- D.1 引言
- D.2 `#include` 预处理器指令
- D.3 `#define` 预处理器指令：符号常量
- D.4 `#define` 预处理器指令：宏
- D.5 条件编译
- D.6 `#error` 和 `#pragma` 预处理器指令
- D.7 运算符 `#` 和 `##`
- D.8 预定义符号常量
- D.9 断言
