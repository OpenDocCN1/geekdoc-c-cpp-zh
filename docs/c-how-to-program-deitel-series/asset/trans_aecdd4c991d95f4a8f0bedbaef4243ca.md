
```cpp
public:
    // constructor
    Count()
        : x(0) // initialize x to 0
    {
        // empty body
    } // end constructor Count

    // output x
    void print() const
    {
        cout << x << endl;
    } // end function print
private:
    int x; // data member
}; // end class Count

// function setX can modify private data of Count
// because setX is declared as a friend of Count (line 9)
void setX( Count &c, int val )
{
    c.x = val; // allowed because setX is a friend of Count
} // end function setX

int main()
{
    Count counter; // create Count object

    cout << "counter.x after instantiation: ";
    counter.print();

    setX( counter, 8 ); // set x using a friend function
    cout << "counter.x after call to setX friend function: ";
    counter.print();
} // end main
```

```text
counter.x after instantiation: 0
counter.x after call to setX friend function: 8
```

**图9.22 |** 友元可以访问类的私有成员。（第2部分，共2部分。）

正如我们提到的，图9.22是使用友元构造的一个机械示例。通常将函数setX定义为类Count的成员函数更为合适。通常也应当将图9.22的程序分成三个文件：

- 1. 一个头文件（例如`Count.h`），包含Count类的定义，而类定义中又包含友元函数setX的原型
- 2. 一个实现文件（例如`Count.cpp`），包含Count类的成员函数定义和友元函数setX的定义
- 3. 一个测试程序（例如`fig09_22.cpp`），包含`main`函数。

## 重载友元函数

可以将重载函数指定为类的友元。每个想要成为友元的函数都必须在类定义中显式地声明为该类的友元。

![](img/b42ba5cd262b1358d16610173f975e4d_447_0.png)

> **软件工程观察 9.12**
> 
> 即使友元函数的原型出现在类定义中，友元也不是成员函数。

![](img/b42ba5cd262b1358d16610173f975e4d_447_1.png)

> **软件工程观察 9.13**
> 
> 私有、保护和公有的成员访问概念与友元声明无关，因此友元声明可以放置在类定义中的任何位置。

![](img/b42ba5cd262b1358d16610173f975e4d_447_2.png)

> **良好编程实践 9.4**
> 
> 将所有友元声明放在类定义体的最前面，并且不要在前面添加任何访问说明符。

## 9.13 使用this指针

我们已经看到，成员函数可以操纵对象的数据。一个类可以有多个对象，那么成员函数如何知道要操纵哪个对象的数据成员呢？每个对象都可以通过一个名为this的指针（一个C++关键字）访问自己的地址。this指针不是对象本身的一部分——也就是说，this指针占用的内存不会反映在对象上的sizeof操作结果中。相反，this指针由编译器作为隐式参数传递给对象的每个非静态成员函数。9.14节将介绍静态类成员，并解释为什么this指针不会隐式传递给静态成员函数。

### 使用this指针避免命名冲突

成员函数隐式地（如我们目前所做的那样）或显式地使用this指针来引用对象的数据成员和其他成员函数。this指针一个常见的显式用法是避免类的数据成员与成员函数参数（或其他局部变量）之间的命名冲突。考虑图9.4–9.5中Time类的hour数据成员和setHour成员函数。我们可以将setHour定义为：

```cpp
// set hour value
void Time::setHour( int hour )
{
    if ( hour >= 0 && hour < 24 )
        this->hour = hour; // use this pointer to access data member
    else
        throw invalid_argument( "hour must be 0-23" );
} // end function setHour
```

在这个函数定义中，setHour的参数与数据成员hour同名。在setHour的作用域内，参数hour隐藏了数据成员。但是，你仍然可以通过使用this->限定其名称来访问数据成员hour。下面的语句将参数hour的值赋给数据成员hour：

```cpp
this->hour = hour; // use this pointer to access data member
```

> **错误预防提示 9.4**
> 
> 为了使你的代码更清晰、更易于维护，并避免错误，绝不要用局部变量名隐藏数据成员。

### `this`指针的类型

`this`指针的类型取决于对象的类型以及使用`this`的成员函数是否声明为const。例如，在类Employee的非const成员函数中，`this`指针的类型为`Employee *`。在const成员函数中，`this`指针的类型为`const Employee *`。

### 隐式和显式使用`this`指针访问对象的数据成员

图9.23演示了隐式和显式使用`this`指针，使类Test的成员函数能够打印Test对象的私有数据x。在下一个示例和第10章中，我们展示了一些使用`this`的重要而微妙的示例。

```cpp
// Fig. 9.23: fig09_23.cpp
// Using the this pointer to refer to object members.
#include <iostream>
using namespace std;

class Test
{
public:
   explicit Test( int = 0 ); // default constructor
   void print() const;
private:
   int x;
}; // end class Test

// constructor
Test::Test( int value )
   : x( value ) // initialize x to value
{
   // empty body
} // end constructor Test

// print x using implicit and explicit this pointers;
// the parentheses around *this are required
void Test::print() const
{
   // implicitly use the this pointer to access the member x
   cout << "\n   x: " << x;

   // explicitly use the this pointer and the arrow operator
   // to access the member x
   cout << "\n   this->x: " << this->x;

   // explicitly use the dereferenced this pointer and
   // the dot operator to access the member x
   cout << "\n(*this).x = " << (*this).x << endl;
} // end function print

int main()
{
    Test testObject( 12 ); // instantiate and initialize testObject

    testObject.print();
} // end main
```

```text
   x: 12
   this->x: 12
(*this).x = 12
```

**图9.23 |** 使用this指针引用对象成员。

为了说明问题，成员函数print（第24–36行）首先使用*this指针隐式地*打印x（第27行）——只指定数据成员的名称。然后print使用两种不同的表示法访问this指针——this指针上的箭头运算符（->）（第31行）和解引用this指针上的点运算符（.）（第35行）。注意与点成员选择运算符（.）一起使用时*this周围的括号（第35行）。这些括号是必需的，因为点运算符的优先级*高于*`*`运算符。没有括号，表达式*this.x会被求值，就像它被括为*(this.x)一样，这是一个*编译错误*，因为点运算符不能与指针一起使用。

this指针的一个有趣用途是防止对象被赋值给自身。正如我们将在第10章中看到的，当对象包含指向动态分配存储的指针时，*自赋值*可能导致严重错误。

### 使用*this*指针启用级联函数调用

this指针的另一个用途是启用级联成员函数调用——即在同一语句中调用多个函数（如图9.26中的第12行）。图9.24–9.26中的程序修改了类Time的set函数setTime、setHour、setMinute和setSecond，使每个函数都返回一个指向Time对象的引用，以启用级联成员函数调用。注意在图9.25中，这些成员函数体中的最后一条语句都将*this（第23、34、45和56行）返回到返回类型`Time &`中。

图9.26中的程序创建了Time对象t（第9行），然后在*级联成员函数调用*（第12和24行）中使用它。为什么将*this作为引用返回的技术能够起作用？点运算符（.）从左到右结合，因此第12行首先计算t.setHour(18)，然后返回对对象t的引用作为该函数调用的值。剩余的表达式随后被解释为：

```cpp
t.setMinute( 30 ).setSecond( 22 );
```

t.setMinute(30)调用执行并返回对对象t的引用。剩余的表达式被解释为：

```cpp
t.setSecond( 22 );
```
