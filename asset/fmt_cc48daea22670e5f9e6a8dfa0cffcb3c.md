
- 许多数学计算都可以使用 C++ 标准库支持的库函数进行。

## 关键术语

`actual arguments` | `argument list` | `bubble sort` | `call by reference` | `call by value` | `called function` | `calling program` | `calling statement` | `cmath` | `const` arguments | `declaration statement` | `default arguments` | `default values` | `dummy variables` | `ellipses` | `empty argument list` | `exit value` | `formal arguments` | `friend` functions | `function call` | `function definition` | `function overloading` | `function polymorphism` | `function prototype` | `indirection` | `inline` | `inline functions` | `macros` | `main()` | `mathlibrary` | `math.h` | `overloading` | `pointers` | `polymorphism` | `prototyping` | `reference variable` | `return by reference` | `return` statement | `return type` | `return()` | `template` | `virtual functions`

## 复习问题

### 认知领域

- 4.1 重述编写原型的不同风格。
- 4.2 指出以下函数原型中的错误，如有：
  (a) `float average(x,y);`
  (b) `int mul(int a,b);`
  (c) `int display(void);`
  (d) `void Vect(int &V, int size);`
  (e) `void print(float data[], size = 20);`
- 4.3 指出使用引用而不是指针的最重要优势。
- 4.4 预测在相关理由下何时应将函数设为 `inline`。
- 4.5 在 `inline` 函数和预处理器宏之间进行区分。
- 4.6 论述在函数中使用默认参数的必要性。

### 使用 C++ 进行面向对象编程

4.7 表达函数声明中空括号的意义。
4.8 重述函数重载。并结合合适的示例说明何时使用这一概念。
4.9 表达实现函数重载的方法。当编译器区分具有相同名称的一组重载函数时，其条件是什么？

### 情感领域

4.10 为以下陈述的正确性辩护：
- (a) 函数参数是由函数返回给调用程序的值。
- (b) 当按值传递参数时，函数使用调用程序中的原始参数进行工作。
- (c) 当函数返回值时，整个函数调用可以分配给变量。
- (d) 函数可以按引用返回值。
- (e) 当参数按引用传递时，调用程序中会创建一个临时变量来保存参数值。
- (f) 在函数原型中不必指定变量名。

4.11 确认按引用传递参数的主要优势。
4.12 综合以下函数定义：

```
(a) int *f( )
{
    int m = 1;
    ...
    return(&m);
}
```

```
(b) double f( )
{
    ...
    return(1);
}
```

```
(c) int & f( )
{
    int n = 10;
    ...
    return(n);
}
```

## 图例

Precision Valuing/Responding/Organizing Applying Remembering Understanding

## 调试练习

4.1 识别以下程序中的错误：

```
#include <iostream>
using namespace std;
int sub(int a=20, int b)
{
    int result;
    result = a - b;
    return result;
}
int main() {
    int a = 100;
    int b = 200;
    int result;
    result = sub(b);
    cout << "value 1 : " << result;
    result = sub(a);
    cout << " value 2 :" << result;
    return 0;
}
```

4.2 识别以下程序段中的错误：

```
int main() {
{
    int a = 2;
    float b = 2.5;
    int show(a);
    float show(b);
    return 0;
}
```

4.3 识别以下程序段中的错误：

```
#include <iostream>
using namespace std;
int p;
int & display();
int main() {
{
    display()=5;
    cout << p ;
    return 0;
}
int & display() {
{
    return 2;
}
```

## 使用 C++ 进行面向对象编程

# 干燥运行练习

4.1 当运行以下程序时会发生什么？

```
#include <iostream>
using namespace std;
int add(int p, int q)
{
    int r;
    r=p+q;
    return r;
}
int main()
{
    int x=7, y=5, z;
    z = add(7,2);
    cout << "Result 1-: " << z << '\\n';
    cout << "Result 2-: " << z + add(7,8) << '\\n';
    cout << "Result 3-: " << add(x,y) << '\\n';
    cout << "Result 4-: " << z << z << '\\n';
}
```

4.2 当以下函数使用 count 的不同值（正值和负值）调用时会发生什么？

```
void fun(int count)
{
    if(count == 0)
        cout <<count;
    else
    {
        cout<<count<<endl;
        fun(--count);
        return;
    }
}
```

4.3 当运行以下程序时会发生什么？

```
#include <iostream>
using namespace std;
int & fun(int &);

int & & fun (int & x)
{
    x++;
    return (x);
}
```

```
int main() {
    int a = 5;
    fun(a) = a;
    cout << a << endl;
    fun(a) = ++a;
    cout << a << endl;
    fun(a) = a++;
    cout << a << endl;
}
```

**4.4** 当运行以下程序时会发生什么？

```
#include <iostream>
Using namespace std;
int main() {
    cout << "Hello" << endl;
    main();
    return 1;
}
```

**4.1** 编写一个函数从键盘读取大小为 `m x n` 的矩阵。
**4.2** 编写一个程序从键盘读取大小为 `m x n` 的矩阵并使用函数在屏幕上显示相同内容。
**4.3** 重写练习 4.2 的程序，使矩阵的行参数成为默认参数。
**4.4** 默认参数的效果可以通过重载来替代实现。用示例讨论。
**4.5** 编写一个宏来获取三个数字中的最大值。
**4.6** 使用内联函数重新做练习 4.5。函数接收值并使用 `main` 程序返回结果。
**4.7** 编写一个函数 `power(r)` 将数字 `m` 提高到幂 `n`。函数对 `m` 采用 `double` 值，对 `n` 采用 `int` 值，并正确返回结果。使用 2 作为 `n` 的默认值，使函数在省略时计算平方。编写一个 `main` 从用户获取 `m` 和 `n` 的值来测试函数。
**4.8** 编写一个执行与练习 4.7 相同操作的函数，但对 `m` 采用 `int` 值。两个函数应具有相同的名称。编写一个 `main` 调用两个函数。使用函数重载的概念。
**4.9** 编写一个程序通过重载 `area(function)` 计算三角形的面积和圆的面积。

## 多项选择题

+ 1. 选择函数声明错误的选项
(a) `int sum (int, float y)`
(b) `float sum (float x, int y)`
(c) `int sum (int x, y)`
(d) `int sum (int, float)`
(a) 4

+ 2. `int &sum(*) { return 2; }` 该函数会返回什么？
(a) 2
(b) 0
(c) error
(d) 1

6. 关于直接递归和间接递归，什么是正确的？

+ 3. 内联函数在以下情况下有效。
(a) 如果函数包含循环、switch 和 goto
(b) 如果函数包含静态变量
(c) 如果递归是递归的
(d) 以上都不对

7. 选择正确的陈述：

+ 4. `float FD (float principle, int=5, float rate)` `amount=FD(2500.50, 7.25)` 上述中哪个参数是默认的？
(a) 第1个
(b) 第2个
(c) 第3个
(d) 无

8. 可以重载的函数：

+ 5. 计算以下输出：

```
#include <iostream>
using namespace std;
inline large (int p, int q)
{return (p>q) ? p : q; }
int main() {
cout << "larger of two is: " 
<< large(4,40) << "\n";
return 0; }
```

9. 编译器可能忽略内联声明的原因是什么？

+ (a) 函数调用自身且函数调用调用函数的函数
(b) 函数调用另一个函数且函数调用调用函数
(c) 函数在两者中都调用自身
(d) 函数在两者中都调用调用者

+ (a) 非尾递归优于尾递归
(b) 尾递归优于非尾递归
(c) 在非尾递归中递归调用是最后一条语句
(d) 链接器在递归中优化

+ (a) 返回类型不同的函数
(b) 具有静态成员函数的函数
(c) 参数声明因 const 而不同
(d) 名称相同但参数不同

+ (a) 太长
(b) 太小
(c) 与普通函数相同
(d) 由于没有参数

+ 10. 单个函数中参数的最大数量是多少？
(a) 127
(b) 128
(c) 253
(d) 256

## 5 类和对象

### 学习目标

阅读本章后，你将能够
- 识别 C++ 结构与 C 结构相比的各种扩展
- 讨论 C++ 程序中类的指定方式
- 解释类的成员函数可以定义的各种方式
- 解释类中如何使用数组
- 讨论静态成员数据和函数的概念
- 说明如何创建对象数组
- 解释友元函数的概念
- 描述如何使用指针访问类的成员

### 5.1 引言

C++ 中最重要的特性是“类”。其重要性体现在 Stroustrup 最初将他的新语言命名为“C with classes”。类是 C 中所使用思想的扩展。它是创建和实现用户定义数据类型的一种新方法。我们将在本章中首先回顾 C 中的传统结构，然后讨论类可以如何设计、实现和应用的概念。

### 5.2 C 结构回顾

我们知道 C 语言的独特特性之一是结构。它们提供了一种将不同类型的数据打包在一起的方法。结构是处理一组逻辑相关数据项的便捷工具。它是一种用户定义的数据类型。一旦结构类型被定义，我们就可以使用类似于内置类型声明的声明来创建该类型的变量。例如，考虑以下声明：

```
struct student {
    char   name[20];
    int    roll_number;
    float total_marks;
};
```

`struct` 将 `student` 声明为一种新的数据类型，可以容纳三种不同数据类型的字段。这些字段称为结构成员或元素。标识符 `student`，被称为结构名称或结构标签，可以使用 `student` 类型的变量创建。例如：

```
struct student A; // C 声明
```

`A` 是 `student` 类型的变量，并且具有模板中定义的三个成员变量。成员变量可以使用点或句点运算符访问，如下所示：

```
strcpy(A.name, "John"); A.roll_number = 999;
A.total_marks = 595.5;
Final_total = A.total_marks + 5;
```

结构可以具有数组、指针或结构作为成员。

#### C 结构的局限性

标准 C 不允许将结构数据类型像内置类型一样对待。例如，考虑以下结构：

```
struct complex {
float x;
float y;
};
struct complex c1, c2, c3;
```

复数 `c1`、`c2` 和 `c3` 可以很容易地使用点运算符赋予值，但我们不能将两个复数相加或从一个中减去另一个。例如，

```
c3 = c1 + c2;
```

在 C 中是非法的。

C 结构的另一个重要局限性是它们不允许数据隐藏。结构成员可以直接被结构变量的任何函数在它们的范围内访问。换句话说，结构成员是公共成员。

#### 对结构的扩展

C++ 支持 C 中定义的结构的全部特性。但 C++ 进一步扩展了其功能以适应其面向对象的理念。它试图将用户定义的类型尽可能接近内置数据类型，并提供隐藏数据的功能，这是面向对象编程的主要原则之一。继承，即一种类型可以继承另一种类型的特征的机制，也得到了 C++ 的支持。

在 C++ 中，结构可以同时具有变量和函数作为成员。它还可以将某些成员声明为“private”，以便外部函数无法直接访问它们。

在 C++ 中，结构名称是独立的，可以像任何其他类型名称一样使用。换句话说，在结构变量的声明中省略关键字 `struct`。例如，我们可以声明 `student` 变量 `A` 为

```
student A; // C++ 声明
```

记住，这在 C 中是错误的。

C++ 将所有这些扩展合并到另一种用户定义的类型中，即类。C++ 中结构和类之间在语法上几乎没有区别，因此它们可以在少量修改下互换使用。由于类是 C++ 中特别引入的数据类型，大多数 C++ 程序员倾向于使用结构仅保存数据，而使用类保存数据和函数。因此，我们将不再进一步讨论结构。

> 注意 C++ 中结构和类之间的唯一区别是，默认情况下类的成员是私有的，而默认情况下结构的成员是公共的。

C++ 中结构和类之间的唯一区别是，默认情况下类的成员是私有的，而默认情况下结构的成员是公共的。

### 5.3 指定类

类是将数据与其相关函数绑定在一起的一种方式。它允许数据（和函数）如果需要的话对外部使用进行隐藏。在定义类时，我们正在创建一个新的抽象数据类型，可以像任何内置数据类型一样对待。一般来说，类规范有两个部分：

1. 类声明
2. 类函数定义

类声明描述其成员的类型和作用域。类函数定义描述类函数如何实现。

类声明的一般形式为：

```
class class_name {
  private:
    variable declarations;
    function declarations;
  public:
    variable declarations;
    function declarations;
};
```

类声明类似于 `struct` 声明。关键字 `class` 指定其后跟的是 `class_name` 的抽象数据类型。类的主体用大括号括起来并以分号结束。类主体包含变量和函数的声明。这些函数和变量统称为类成员。它们通常分为两种类型，即 `private` 和 `public`，以表示哪些成员是私有的，哪些是公共的。关键字 `private` 和 `public` 被称为可见性标签。请注意关键字后跟冒号。

已声明的类成员只能从类内部访问。另一方面，公共成员也可以从类外部访问。数据隐藏（使用 `private` 声明）是面向对象编程的关键特性。关键字 `private` 的使用是可选的。默认情况下，类的成员是私有的。如果两个标签都缺失，则默认情况下所有成员都是私有的。这样的类完全对外部世界隐藏，没有任何作用。

类内部声明的变量称为数据成员，函数称为成员函数。只有成员函数可以访问私有数据成员和私有函数。然而，公有成员（函数和数据）可以从类外部访问。这在图 5.1 中有所说明。将数据和函数绑定到单个类类型变量中称为封装。

## CLASS

![](img/20ee75c0321e4c9269cadbf08d7acd34_121_0.png)

图 5.1 类中的数据隐藏

#### 一个简单的类示例

典型的类声明看起来像：

```cpp
class item
{
    int number; // variables declaration
    float cost; // private by default
public:
    void getdata(int a, float b); // functions declaration
    void putdata(void);          // using prototype
};
```
