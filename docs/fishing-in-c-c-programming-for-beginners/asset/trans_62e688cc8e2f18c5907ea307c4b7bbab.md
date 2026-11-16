

int main ()
{
    try
    {
        long double*array=new long double[100000000000000000];
    }
    catch (exception& e)
    {
        cout << "Here is an error: " << e.what()<< endl;
    }

    return 0;
}
```

输出

Here is an error: std::bad_alloc

我们可以抛出预先决定的错误，此外还可以决定 what() 函数显示的内容。

考虑以下程序：

```
#include <iostream>
#include <exception>
using namespace std;
class myexception: public exception
{
    virtual const char* what() const throw()
    {
        return "My exception occured";
    }
}
myexample;
int main ()
{
    try
    {
        throw myexample;
    }
    catch (exception& e)
    {
        cout << e.what() << endl;
    }

    return 0;
}
```

输出

My exception occurred

![](img/5340985153962870d4e4a3b9453b9146_249_0.png)

## 命名空间

是否可以定义两个同名但数据类型不同的变量？

考虑以下程序：

```
#include<iostream>
int main()
{
    int var=3;
    float var=5;
    cout<<var;
}
```

该程序将显示错误：“[Error] conflicting declaration ‘float var’”。

但是，可以使用命名空间定义两个同名变量！

要声明命名空间，我们使用以下语法：

```
namespace namespace_name
{
//statements
}
```

编写上述行后，我们编写的所有内容都属于此命名空间。

如果我们在另一个命名空间中，则使用域运算符 (::) 来访问该命名空间的元素。

考虑以下程序：

```
#include<iostream>
using namespace std;
namespace ns1
{
    int var=3;
}
namespace ns2
{
    float var=5;
}
int main()
{
    cout<<ns1::var<<endl;
    cout<<ns2::var;
}
```

输出

3

5

但是，请记住 Turbo C++ 不支持 **命名空间** 关键字。如果你使用 Turbo C++，那么本章中实现的各种程序将无法工作。你应当立即放弃它，切换到 Borland C++ 编译器。你可以切换到 Dev C++、Code::Blocks 以及其他各种流行编译器。所有这些都是免费且易于使用的。

这里，你可以看到访问每个元素时我们使用了域运算符 (::)。为每个元素都使用此运算符是一项繁琐的工作。因此使用了关键字 **using**。

### using 关键字

这是一个多用途关键字。它有两种用途：一种是在程序中访问命名空间，另一种是在程序中使用特定命名空间的变量。

### 访问命名空间

using 的语法如下：

```
using namespace namespace_name;
```

一旦声明上述语句，后续语句将被视为属于该命名空间，除非遇到另一条类似的上述语句。

考虑以下程序：

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
    int b=2;
}
namespace ns2
{
    float a=3.33;
    double b=4.44;
}
int main()
{
    using namespace ns1;
    cout<<a<<endl;
    cout<<b;
}
```

输出
1
2

### 使用特定命名空间的元素

此处语法如下：

```
using namespace_name::element_name;
```

考虑以下程序：

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
    int b=2;
    int add(int x,int y){return x+y;}
}
namespace ns2
{
    float a=3.33;
    double b=4.44;
    int add(int x,int y){return 2*x+y;}
}
int main()
{
    using ns1::a;
    using ns1::b;
    using ns1::add;
    cout<<a<<endl;
    cout<<b<<endl;
    cout<<add(a,b);
}
```

输出
1
2
3

### 同时使用多个命名空间

命名空间还允许我们同时使用多个命名空间。我们可以告诉编译器使用一个命名空间的变量和另一个命名空间的其他变量。

考虑以下程序：

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
    int b=2;
}
namespace ns2
{
    float a=3.33;
    double b=4.44;
}
int main()
{
    using ns1::a;
    using ns2::b;
    cout<<a<<endl;
    cout<<b;
}
```

输出

1

4.44

这里，你可以看到 ns1::a 不是命名空间，而是一个变量。因此，我们不能使用 using namespace ns1::a；这里，a 来自 ns1，b 来自 ns2。

现在考虑以下程序：

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
}
namespace ns2
{
    float a=3.33;
}
int main()
{
    using namespace ns1;
    cout<<a<<endl;
    using namespace ns2;
    cout<<a<<endl;
}
```

该程序将生成错误，因为包含命名空间并不意味着删除之前的命名空间。因此，变量 a 是歧义的。但是，命名空间仅在整个块内有效，块外无效。因此，你可以按以下方式编写上述程序：

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
}
namespace ns2
{
    float a=3.33;
}
int main()
{
    {
        using namespace ns1;
        cout<<a<<endl;
    }
    {
        using namespace ns2;
        cout<<a<<endl;
    }
}
```

输出
1
3.33

### 命名空间别名

命名空间的一个惊人特性是可以为其创建别名。创建别名后，旧名称和新名称都可以使用。

重命名命名空间的语法如下：

```
namespace new_name=old_name;
```

考虑以下程序：

```
#include<iostream>
using namespace std;
namespace ns1
{
    int a=1;
}
namespace ns2=ns1;
int main()
{
    using namespace ns1;
    cout<<a<<endl;
    using namespace ns2;
    cout<<a;
}
```

输出

1
1

这次变量 a 不是歧义的。

![](img/5340985153962870d4e4a3b9453b9146_257_0.png)

## 模板

模板，也称为“泛型”或“参数化类型”，使你能够构建一组相关的函数或类。当你需要编写大量几乎相同的内容时，会使用它。这是 C++ 的一项特殊功能，属于其 **代码重用和回收** 属性。在这里，你将看到如何高效地重用代码。

假设我们定义如下函数：

```
int random(int a, int b)
{
    return a+b+sizeof(int);
}
```

一个非常简单的函数，对吧！现在，假设我们不仅希望上述函数适用于整数，还希望在程序中适用于 double、short 和 long double 数据类型。这里出现了一个问题，我们需要为每个对应的数据类型定义四个不同的函数。难道就没有方法来减少这项工作吗？这时模板就很有用了。

首先，我们来看看这个繁琐的程序，然后我们将使用模板对其进行简化：

```
#include<iostream>
using namespace std;
short random(short a,short b)
{
    return a+b+sizeof(short);
}
int random(int a,int b)
{
    return a+b+sizeof(int);
}
double random(double a,double b)
{
    return a+b+sizeof(double);
}
long double random(long double a,long double b)
{
    return a+b+sizeof(long double);
}

int main()
{
    short xa=5,ya=6;
    int xb=5,yb=6;
    double xc=5,yc=6;
    long double xd=5,yd=6;
    short p=random(xa,ya);
    int q=random(xb,yb) ;
    double r=random(xc,yc);
    long double s=random(xd,yd);
    cout<<p<<endl<<q<<endl<<r<<endl<<s<<endl;
}
```

| 64 位编译器上的输出 | 32 位编译器上的输出 |
| :--- | :--- |
| 13 | 13 |
| 15 | 13 |
| 19 | 19 |
| 27 | 21 |

你现在已经了解，在定义模板时，我们需要针对数据类型而非值进行工作。我们可以说，我们将定义一个以数据类型作为参数并对值进行操作的模板，而不考虑其数据类型。

模板有两种类型

- 1. 函数模板
- 2. 类模板

### 函数模板

函数模板可以通过两种方式定义，即使用两个不同的关键字 class 和 typename。两者可以以相同的方式使用。

声明模板的语法如下：

```
template <typename identifier> function_declaration;
```

另一种非常流行的语法是：

```
template <class identifier> function_declaration;
```

因此，声明示例可以是：

```
template <class myDataType> myDataType GetMax(myDataType a, myDataType b);
```

```
template <typename myDataType> myDataType GetMax(myDataType a, myDataType b);
```

函数模板可以像其他函数一样定义，但不同之处在于我们不使用 int、float 等，而是到处使用 myDataType。

因此，上面定义的 random 函数的相应定义将是：

```
template <typename T>

T random(T a, T b)

{
     return a+b+sizeof(T);
}
```

但是，请记住 Turbo C++ 不支持 typename 关键字。如果你使用 Turbo C++，那么本章中实现的各种程序将无法工作，因为 Turbo C++ 未更新。你应当立即放弃它，切换到 Borland C++ 编译器。你可以切换到 Dev C++、Code::Blocks 以及其他各种流行编译器。所有这些都是免费且易于使用的。

我们还可以在函数定义中创建对象。因此，上面的代码片段也可以写成：

```
template <typename T>

T random(T a, T b)
```

