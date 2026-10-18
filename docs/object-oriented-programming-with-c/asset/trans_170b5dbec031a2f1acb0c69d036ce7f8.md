
声明的方式与普通变量的初始化非常相似。例如，

```cpp
int m = 20;
float x = 5.75;
```
`

这些都是基本数据类型的有效初始化语句。

类似地，当内置类型的变量超出作用域时，编译器会自动销毁该变量。但到目前为止我们所研究的对象并没有发生这种情况。因此，显然还需要探索类的更多特性，使我们能够在对象创建时初始化它们，并在不再需要它们时销毁它们。

C++ 提供了一种称为构造函数（constructor）的特殊成员函数，它使对象在创建时能够自行初始化。这被称为对象的*自动初始化*。C++ 还提供了另一种称为*析构函数*（destructor）的成员函数，用于在不再需要对象时销毁它们。

## 6.2 构造函数

**构造函数是一种“特殊”的成员函数，其任务是初始化其类的对象。** 它之所以特殊，是因为它的名称与类名相同。每当创建其关联类的对象时，构造函数就会被调用。它被称为构造函数，是因为它构造了类的数据成员的值。

构造函数的声明和定义如下：

```cpp
// class with a constructor
class integer
{
    int m, n;
public:
    integer(void); // constructor declared
    ...
    ....
};
integer :: integer(void) // constructor defined
{
    m = 0; n = 0;
}
```

当一个类包含如上定义的构造函数时，该类创建的对象将保证被自动初始化。例如，声明

```cpp
integer int1; // object int1 created
```

不仅创建了 integer 类型的对象 int1，还将其数据成员 m 和 n 初始化为零。无需编写任何语句来调用构造函数（正如我们对普通成员函数所做的那样）。如果为归零初始化定义了一个“普通”成员函数，则需要为每个对象分别调用该函数。如果对象数量很大，这将非常不方便。

不接受参数的构造函数称为*默认构造函数*。**类 A** 的默认构造函数是 **A::A( )**。如果没有定义这样的构造函数，编译器会提供一个默认构造函数。因此，如下语句

```
A a;
```

会调用编译器的默认构造函数来创建对象 a。

构造函数具有一些特殊特性。它们是：

- 它们应在 public 部分声明。
- 它们在创建对象时自动调用。

- 它们没有返回类型，甚至没有 void，因此不能返回值。
- 它们不能被继承，尽管派生类可以调用基类构造函数。
- 与其他 C++ 函数一样，它们可以有默认参数。
- 构造函数不能是**虚拟**的。（虚拟的含义将在第 9 章后面讨论。）
- 我们不能引用它们的地址。
- 带有构造函数（或析构函数）的对象不能用作联合体的成员。
- 当需要内存分配时，它们会对运算符 **new** 和 **delete** 进行“隐式调用”。

请记住，当为一个类声明构造函数时，该类的对象初始化就变得必不可少。

## 6.3 参数化构造函数

上面定义的构造函数 **integer()** 将所有对象的数据成员初始化为零。然而，在实践中，可能需要在创建不同对象时，用不同的值来初始化它们的不同数据元素。C++ 允许我们在创建对象时向构造函数传递参数来实现这一目标。可以接受参数的构造函数称为*参数化构造函数*。

构造函数 **integer()** 可以修改为接受参数，如下所示：

```cpp
class integer {
    int m, n;
public:
    integer(int x, int y); // parameterized constructor
    ....
    ....
};
```

当构造函数被参数化后，类似这样的对象声明语句

```
integer int1;
```

可能无法工作。在声明对象时，我们必须将初始值作为参数传递给构造函数。这可以通过两种方式完成：

- 通过显式调用构造函数。
- 通过隐式调用构造函数。

下面的声明说明了第一种方法：

```cpp
integer int1 = integer(0,100); // explicit call
```

该语句创建一个 integer 对象 int1，并将值 0 和 100 传递给它。第二种方法实现如下：

```cpp
integer int1(0,100); // implicit call
```

这种方法有时称为简写方法，由于它更简短、看起来更好且易于实现，因而经常使用。

请记住，当构造函数被参数化时，我们必须为构造函数提供适当的参数。程序 6.1 演示了如何向构造函数传递参数。

## 程序 6.1 带构造函数的类

```cpp
#include <iostream>
using namespace std;
class integer
{
int m, n;
public:
integer(int, int); // constructor declared

void display(void)
{
cout << “ m = “ << m << “\n”
cout << “ n = “ << n << “\n”
}
};
integer :: integer(int x, int y) // constructor defined
{
m = x; n = y;
}
int main( )
{
integer int1(0,100); // constructor called implicitly
integer int2 = integer(25, 75); // constructor called explicitly
cout << “\nOBJECT1” << “\n”
int1.display( );
cout << “\nOBJECT2” << “\n”
int2.display( );
return 0;
}
```

程序 6.1 的输出将是：

```
OBJECT1
m = 0 n = 100

OBJECT2
```

m = 25
n = 75

构造函数也可以定义为**内联**函数。
例如：

```cpp
class integer
{
int m, n;
public:
integer(int x, int y)  // inline constructor
{
m = x; y = n;
}
. . . .
};
```

构造函数的参数可以是任何类型，但不能是其所属类的类型。例如，

```cpp
class A
{
. . . .
. . . .
public:
A(A);
};
```

这是非法的。

然而，构造函数可以接受对其自身类的*引用*作为参数。因此，语句

```cpp
Class A
{
. . . .
. . . .
```

public:
A(A&);
};

是有效的。在这种情况下，该构造函数称为_复制构造函数_。

## 6.4 类中的多个构造函数

到目前为止，我们已经使用了两种构造函数。它们是：

+   integer( ); // 无参数
+   integer( int ); // 两个参数

在第一种情况下，构造函数本身提供数据值，调用程序不传递任何值。在第二种情况下，函数调用从 main( ) 传递适当的值。C++ 允许我们在同一个类中使用这两种构造函数。例如，我们可以如下定义一个类：

```cpp
class integer
{
int m, n;
public:
integer( ){m=0; n=0;} // constructor 1
integer( int a, int b)
{m = a; n = b;} // constructor 2
integer( integer & i)
{m = i.m; n = i.n;} // constructor 3
};
```

这为一个 integer 对象声明了三个构造函数。第一个构造函数不接受参数，第二个接受两个整数参数，第三个接受一个 integer 对象作为参数。例如，声明

```
integer l1;
```

将自动调用第一个构造函数，并将 **m** 和 **n**（即 I1 的 m 和 n）都设为零。语句

```
integer I2(20,40);
```

将调用第二个构造函数，它分别将数据成员 **m** 和 **n**（即 I2 的 m 和 n）初始化为 20 和 40。最后，语句

```
integer I3(I2);
```

将调用第三个构造函数，它把 I2 的值复制到 I3 中。换句话说，它将 I3 的每个数据元素的值设置为 I2 对应数据元素的值。如前所述，这样的构造函数称为*复制构造函数*。我们在第 4 章中学到，两个或更多函数共享相同名称的过程称为函数重载。类似地，当一个类中定义了多个构造函数时，我们就说构造函数被重载了。

程序 6.2 展示了重载构造函数的使用。

## 程序 6.2 重载构造函数

```cpp
#include <iostream>
using namespace std;
class complex
{
float x, y;
public:
complex( ) { }  // *constructor no arg*
complex(float a) {x = y = a;}  // *constructor-one arg*
complex(float real, float imag)  // *constructor-two args*
{x = real; y = imag;}
friend complex sum(complex, complex);
```
