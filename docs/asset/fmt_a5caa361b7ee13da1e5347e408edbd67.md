
```cpp
#include <iostream>
using namespace std;

class sample
{
    int a;
    int b;
    public:
        void setvalue() {a=25; b=40; }
        friend float mean(sample s);
};
float mean(sample s)
{
    return float(s.a + s.b)/2.0;
}

int main()
{
    sample X;    // object X
    X.setvalue();
    cout << "Mean value = " << mean(X) << "\n";

    return 0;
}
```

程序 5.8 的输出为：

```
Mean value = 32.5
```

注意

> 友元函数通过点运算符以及传递给它的对象来访问类变量 `a` 和 `b`。函数调用 `mean(X)` 按值将对象 `X` 传递给友元函数。

一个类的成员函数可以是另一个类的友元函数。在这种情况下，它们使用作用域运算符进行定义，如下所示：

```
class X
{
    .....
    .....
    int fun1();    // member function of X
    .....
};

class Y
{
    .....
    .....
    friend int X :: fun1();      // fun1() of X
                                 // is friend of Y
    .....
};
```

函数 `fun1()` 是 `类 X` 的成员，也是类 `Y` 的一个 `友元`。

我们还可以将一个类的所有成员函数声明为另一个类的友元函数。在这种情况下，该类称为 `友元类`。这可以如下指定：

```
class Z
{
    .....
    friend class X;    // all member functions of X are
                      // friends to Z
};
```

程序 5.9 演示了友元函数如何充当类之间的桥梁。

### 对两个类友好的函数

```
#include <iostream>

using namespace std;

class ABC;    // Forward declaration
//--------------------------------------------------//
class XYZ
{
    int x;
public:
    void setvalue(int i) {x = i;}
    friend void max(XYZ, ABC);
};
//--------------------------------------------------//
class ABC
{
    int a;
public:
    void setvalue(int i) {a = i;}
    friend void max(XYZ, ABC);
};
```

### 交换类的私有数据

```cpp
#include <iostream>
using namespace std;

class class_2;

class class_1
{
	int value1;
public:
	void indata(int a) {value1 = a;}
	void display(void) {cout << value1 << "\n";}
	friend void exchange(class_1 &, class_2 &);
};

class class_2
{
	int value2;
public:
	void indata(int a) {value2 = a;}
	void display(void) {cout << value2 << "\n";}
	friend void exchange(class_1 &, class_2 &);
};

void exchange(class_1 &x, class_2 &y)
{
	int temp = x.value1;
	x.value1 = y.value2;
	y.value2 = temp;
}

int main()
{
	class_1 C1;
	class_2 C2;
	C1.indata(100);
	C2.indata(200);
	cout << "Values before exchange" << "\n";
	C1.display();
	C2.display();
	exchange(C1, C2);      // swapping

	cout << "Values after exchange " << "\n";
	C1.display();
	C2.display();

	return 0;
}
```

**程序 5.10**

对象 `x` 和 `y` 分别是 `C1` 和 `C2` 的别名。以下语句

```
int temp = x.value1;
x.value1 = y.value2;
y.value2 = temp;
```

直接修改了 `class_1` 和 `class_2` 中声明的 `value1` 和 `value2` 的值。

以下是程序 5.10 的输出：

```
Values before exchange
100
200
Values after exchange
200
100
```

## 5.16 返回对象

函数不仅可以接收对象作为参数，还可以返回对象。程序 5.11 中的示例说明了如何（在函数内部）创建对象并将其返回给另一个函数。

### 返回对象

```cpp
#include <iostream>

using namespace std;

class complex      // x + iy form
{
    float x;        // real part
    float y;        // imaginary part
public:
    void input(float real, float imag)
    { x = real; y = imag; }
    friend complex sum(complex, complex);
    void show(complex);
};

complex sum(complex c1, complex c2)
{
    complex c3;            // objects c3 is created
    c3.x = c1.x + c2.x;
    c3.y = c1.y + c2.y;
    return(c3);            // returns object c3
}

void complex :: show(complex c)
{
    cout << c.x << " + j" << c.y << "\n";
}

int main()
{
    complex A, B, C;

    A.input(3.1, 5.65);
    B.input(2.75, 1.2);

    C = sum(A, B);          // C = A + B

    cout << "A = "; A.show(A);
    cout << "B = "; B.show(B);
    cout << "C = "; C.show(C);

    return 0;
}
```

程序 5.11 执行后将生成以下输出：

```
A = 3.1 + j5.65
B = 2.75 + j1.2
C = 5.85 + j6.85
```

该程序将两个复数 `A` 和 `B` 相加，得到第三个复数 `C`，并显示这三个数。

## 5.17 常量成员函数

如果成员函数不修改类中的任何数据，则可以将其声明为常量成员函数，如下所示：

```
void mul(int, int) const;
double get_balance() const;
```

限定符 `const` 附加在函数原型（声明和定义中都要）之后。如果此类函数试图修改数据值，编译器将生成错误消息。

## 5.18 指向成员的指针

可以获取类成员的地址并将其赋给指针。可以通过对“完全限定”的类成员名应用运算符 `&` 来获取成员的地址。可以使用运算符 `::*` 和类名来声明类成员指针。例如，给定类

```
class A
{
    private:
        int m;
    public:
        void show();
};
```

我们可以如下定义指向成员 `m` 的指针：

```
int A::* ip = &A :: m;
```

这样创建的指针 `ip` 的行为类似于类成员，因为它必须使用类对象来调用。在上面的语句中，`A::*` 表示“指向 `A` 类成员的指针”。`&A::m` 表示“`A` 类成员 `m` 的地址”。

请记住，以下语句是无效的：

```
int *ip = &m;    // 不起作用
```

这是因为 `m` 不仅仅是 `int` 类型的数据。只有与它所属的类关联时，它才有意义。作用域运算符必须同时应用于指针和成员。

现在可以使用指针 `ip` 在成员函数（或友元函数）中访问成员 `m`。假设 `a` 是在成员函数中声明的 `A` 类对象。我们可以如下使用指针 `ip` 访问 `m`：

```
cout << a.*ip;    // 显示
cout << a.m;      // 与上面相同
```

现在，看下面的代码：

```
ap = &a;                 // ap 是指向对象 `a` 的指针
cout << ap -> *ip;       // 显示 `m`
cout << ap -> m; // 与上面相同
```

当同时使用指向对象和成员的指针时，使用解引用运算符 `->*` 来访问成员。当对象本身与成员指针一起使用时，使用解引用运算符 `.*`。请注意，`*ip` 的使用方式类似于成员名。

我们还可以设计指向成员函数的指针，然后可以在 `main` 中使用解引用运算符调用它们，如下所示：

```
(对象名 .* 指向成员函数的指针) (10);
(指向对象的指针 ->* 指向成员函数的指针) (10)
```

`()` 的优先级高于 `.*` 和 `->*`，因此括号是必需的。

程序 5.12 演示了使用解引用运算符访问类成员。

### 解引用运算符

```cpp
#include <iostream>

using namespace std;

class M
{
    int x;
    int y;
public:
    void set_xy(int a, int b)
    {
        x = a;
        y = b;
    }
    friend int sum(M m);
};

int sum(M m)
{
        int M:: *px = &M::x;
        int M:: *py = &M::y;
        M *pm = &m;
        int S = m.*px + pm->*py;
        return S;
}

int main()
{
        M m;
        void (M:: *pf)(int,int) = &M::set_xy;
        (m.*pf)(10,20);
        cout << "SUM = " << sum(m) << "\n";
        M *pm = &m;
        (pm->*pf)(30,40);
        cout << "SUM = " << sum(m) << "\n";
        return 0;
}
```

程序 5.12 的输出为：

```
SUM = 30
SUM = 70
```

## 5.19 局部类

可以在函数或块内部定义和使用类。这样的类称为局部类。示例：

```cpp
void test(int a)       // 函数
{
    .....
    .....
    class student;  // 局部类
    {
            .....
            .....  // 类定义
    }

    student s1(a);      // 创建 student 对象
    ....              // 使用 student 对象
}
```

局部类可以使用全局变量（在函数上方声明的变量）和在函数内部声明的静态变量，但不能使用自动局部变量。全局变量应使用作用域运算符（`::`）。

构造局部类时存在一些限制。它们不能有静态数据成员，并且成员函数必须在局部类内部定义。外部函数不能访问局部类的私有成员。但是，可以通过将外部函数声明为友元来实现这一点。

## 摘要

- ↔ 类是结构数据类型的扩展。类可以同时将变量和函数作为成员。
- ↔ 默认情况下，类的成员是私有的，而结构的成员是公有的。
- ↔ 只有成员函数可以访问私有数据成员和私有函数。然而，公有成员可以从类外部访问。
- ↔ 在 C++ 中，类变量称为对象。通过对象，我们可以使用点运算符访问类的公有成员。
- ↔ 我们可以在类的内部或外部定义成员函数。成员函数与普通函数的区别在于，成员函数在函数头中使用成员“标识”标签来指明它所属的类。
- ↔ 对象的内存空间在声明时分配。成员变量的空间为每个对象单独分配，但成员函数不分配单独的空间。
- ↔ 类的数据成员可以声明为静态的，通常用于维护整个类共有的值。
- ↔ 静态成员变量必须在类外部定义。
- ↔ 静态成员函数可以访问在同一个类中声明的静态成员，并且可以使用类名调用。
- ↔ C++ 允许我们有对象数组。
- ↔ 我们可以使用对象作为函数参数。
- ↔ 声明为 `友元` 的函数不在它被声明为友元的类的作用域内。它可以完全访问该类的私有成员。
- ↔ 函数也可以返回对象。
- ↔ 如果成员函数不修改类中的任何数据，则可以将其声明为 `常量` 成员函数。关键字 `const` 附加在函数原型之后。
- ↔ 也可以在函数内部定义和使用类。这样的类称为局部类。

## 关键术语

- 抽象数据类型
- 对象数组
- `类`
- 类声明
- 类成员
- 类变量
- `常量` 成员函数
- 数据隐藏
- 数据成员
- 解引用运算符
- 点运算符
- 元素
- 封装
- `友元` 函数
- 继承
- `内联` 函数
- 局部类
- 成员函数
- 成员函数的嵌套
- 对象
- 按引用传递
- 按值传递
- 句点运算符
- `私有`
- 原型
- `公有`
- 作用域运算符
- 作用域解析
- `静态` 数据成员
- 静态成员函数
- 静态变量
- `结构体`
- 结构
- 结构成员
- 结构名称
- 结构标记
- 模板

## 复习题

- 5.1 C 和 C++ 中的结构有何不同？
- 5.2 什么是类？它如何实现数据隐藏？
- 5.3 C++ 结构体与 C++ 类有何不同？
- 5.4 什么是对象？它们是如何创建的？
- 5.5 如何定义类的成员函数？
- 5.6 在同一个程序文件中，可以将相同的函数名用于类的成员函数和外部函数吗？如果可以，如何区分它们？如果不可以，请说明理由。
- 5.7 描述在以下情况下访问数据成员和成员函数的机制：
  - (a) 在 `main` 程序内部。
  - (b) 在同一个类的成员函数内部。
  - (c) 在另一个类的成员函数内部。
- 5.8 我们何时将类的成员声明为静态的？
- 5.9 什么是友元函数？使用友元函数的优点和缺点是什么？
- 5.10 判断下列说法是正确（TRUE）还是错误（FALSE）。
  - (a) 类中的数据项必须总是私有的。
  - (b) 设计为私有的函数只能被该类的成员函数访问。
  - (c) 设计为公有的函数可以像其他普通函数一样被访问。
  - (d) 在类说明符内部定义的成员函数默认成为内联函数。
  - (e) 类可以将一个实体的所有方面汇集在一个地方。
  - (f) 类成员默认是公有的。
  - (g) 友元函数只能访问类的公有成员。
  - (h) 可以使整个类成为另一个类的友元。
  - (i) 函数不能返回类对象。
  - (j) 可以在类说明符内部初始化数据成员。

## 调试练习

5.1 找出以下程序中的错误。

```cpp
#include <iostream.h>

struct Room
{
    int width;
    int length;
}

void setValue(int w, int l)
{
    width = w;
    length = l;
}

void main()
{
    Room objRoom;
    objRoom.setValue(12, 1,4);
}
```

### 5.2 识别以下程序中的错误。

```cpp
#include <iostream.h>

class Room
{
    int width, height;
    void setValue(int w, int h)
    {
        width = w;
        height = h;
    }
};

void main()
{
    Room objRoom;
    objRoom.width = 12;
}
```

### 5.3 识别以下程序中的错误。

```cpp
#include <iostream.h>

class Item
{
```
