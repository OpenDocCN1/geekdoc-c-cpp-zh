

using namespace std;
int main()
{
    cout<<x;
}
int x=5;

这个程序会生成一个错误 "x was not declared in this scope"

现在，让我们稍微修改一下代码，如下所示：

#include<iostream>
using namespace std;
int main()
{
    extern int x;
    cout<<x;
}
int x=5;

现在，这个程序将成功执行，输出结果为 5。

## 默认参数

函数可以有默认参数。如果未为它们传递参数，则这些参数会自动使用。默认参数在函数声明中声明。例如，请考虑以下程序：

#include<iostream>
using namespace std;
int add(int x=1,int y=2);
int main()
{
    cout<<add()<<endl;
    cout<<add(5)<<endl;
    cout<<add(5,6);
}
int add(int x,int y)
{
 return x+y;
}

输出
3
7
11

请看这里，在第一次调用函数时，由于我们没有传递任何值，因此自动使用了函数声明中的 1 和 2。在第二次调用时，我们传递了一个值，因此该值被视为第一个参数，于是 5 和 2 相加得到 7。然后在第三次调用时，我们将两个参数都传递给了函数，因此返回了结果 11。

请注意，函数声明中包含默认参数，而不是函数定义。

## 函数重载

C++ 有能力根据传递给它们的参数类型来区分不同的函数。这使我们能够使用同名的多个函数。

请考虑以下程序：

#include<iostream>
using namespace std;
void disp();
void disp(int);
void disp(char);
void disp(int,char);
int main()
{
    int i=5;
    char ch='c';
    disp(i,ch);
    disp(i);
    disp();
    disp(ch);
}
void disp()
{
    cout<<"In 1"<<endl;
}
void disp(int x)
{
    cout<<"In 2"<<endl;
}
void disp(char c)
{
    cout<<"In 3"<<endl;
}
void disp(int x,char c)
{
    cout<<"In 4"<<endl;
}

输出
In 4
In 2
In 1
In 3

看，编译器是多么高效地自动决定使用哪个函数。它只是将参数类型与要调用的函数进行匹配。这称为函数重载。

## 内联函数

在调用函数时，控制权会跳转到函数，执行其中的语句，然后返回到 main() 函数。再次调用函数时，同样的过程会重复。此过程有两个缺点：

- 1. 相比于没有函数的程序，它稍微更耗时
- 2. 它打断了连续性

为了解决这些问题，我们使用一种称为内联函数的安排。如果我们将函数声明为内联，那么我们实际上是在建议编译器将函数中编写的语句复制到调用函数本身，而不是调用函数。函数不一定会被内联，但大多数非常小的函数在声明为内联时都会被内联。

内联函数的语法：

inline return_type func_name(data_type1 arg1,data_type2 arg2,...)
{
/*Statements*/
}

以下程序说明了如何使用内联函数：

#include<iostream>
using namespace std;
inline int add(int a,int b);
int main()
{
for(int i=0;i<1000;i++)
cout<<add(5,6);
return 0;
}
inline int add(int a,int b)
{
    return a+b;
}

![](img/5340985153962870d4e4a3b9453b9146_87_0.png)

## 指针

本部分包含两个特殊符号 & 和 *

& - 它称为变量的地址。

请考虑以下程序：

#include<iostream>
using namespace std;
int main()
{
    int a=5;
    cout<<&a;
    return 0;
}

在这里，它将显示存储变量的内存地址。输出取决于编译器，在我的编译器中它显示了 0x22fe4c。在你的编译器中，可能会不同。

* 星号，也称为地址处的值，用于访问存储在变量地址处的值。

指针可以声明为

int *a;

请考虑以下程序：

#include<iostream>
using namespace std;
int main()
{
    int *a;
    cout<<*a;
    return 0;
}

在这个程序中，我们没有给 a 分配任何地址，但我们正在尝试访问该地址处存储的值。这会简单地导致程序崩溃，输出如下：

![](img/5340985153962870d4e4a3b9453b9146_89_0.png)

请考虑以下程序

#include<iostream>
using namespace std;
int main()
{
    int b=5;
    int *a=&b;
    cout<<*a;
    return 0;
}

这个程序将把 b 的地址赋给 a，而不是看起来那样赋给 *a。因此，输出将显示为 5

为了消除混淆，int *a = &b; 也可以写成：

int *a;
a=&b;

现在，如果你像下面的程序那样更改 a 处存储的值，那么地址处的值将被更改。

#include<iostream>
using namespace std;
int main()
{
    int b=5;
    int *a=&b;
    cout<<*a;
    *a=7;
    cout<<endl<<b;
    cout<<endl<<*a;
}

输出：
5
7
7

这个程序说明了这样一个事实：无论我们通过指针进行什么更改，更改都会发生在内存地址处。

请考虑以下程序：

#include<iostream>
using namespace std;
int display1(int *x);
int main()
{
    int a=5;
    cout<<a;
    display1(&a);
    cout<<a;
}
int display1(int *x)
{
*x = 6;
}

上面程序的输出将是 56。因为我们使用取地址运算符将地址传递给了函数 display1()。在那里，我们使用了指针，以便它可以接收地址。然后使用解引用运算符，我们将 a 地址处的值更改为 6。当我们在 main() 函数中打印相同的值时，我们可以看到 main() 函数中的值也已更改。

## 按值调用和按引用调用

函数可以以两种方式调用

- 1. 按值调用
- 2. 按引用调用

按引用调用又可以细分为两部分

- i. 使用指针调用
- ii. 不使用指针调用

## 按值调用

当我们按值调用函数时，会创建传递给函数的局部变量的副本并将其传递给函数。因此，函数执行后，局部变量的原始值不会改变。

例如，请考虑以下程序

#include<iostream>
using namespace std;
int display1(int);
int main()
{
    int a=5;
    display1(a);
    cout<<a;
}
int display1(int a)
{
a = 6;
}

在这个程序中，输出将是 5，尽管我们在 display1() 函数中将 a 的值更改为了 6。这称为按值调用函数。在这里，a 值的一个副本被传递给 display1() 函数。因此，main() 函数中的值保持不变，因为原始地址处存储的值没有被更改，而是 display1() 函数中的值的副本被更改了，并且此更改将持续存在，直到函数 display1() 将控制权返回给 main()。

如果上述说法正确，那么如果我们尝试在以下程序中访问 num 的内存位置，它应该给出两个不同的值，这可以轻松查看。

![](img/5340985153962870d4e4a3b9453b9146_92_0.png)

## 使用指针的按引用调用

当我们通过使用指针或使用地址按引用调用函数时，变量的地址会被传递给函数。因此，无论我们在函数中做什么更改，相同的更改都会发生在局部变量的原始内存位置。

请考虑以下程序：

#include<iostream>
using namespace std;
int display1(int*);
int main()
{
    int a=5;
    cout<<a;
    display1(&a);
    cout<<a;
}
int display1(int *x)
{
*x = 6;
}

上面程序的输出将是 56。因为我们使用取地址运算符将地址传递给了函数 display1()。因此，这称为按引用调用函数。

## 不使用指针的按引用调用

我们也可以不使用地址来按引用调用函数。

例如，请考虑以下程序：

#include<iostream>
using namespace std;
int display1(int &);
int main()
{
int a=5;
cout<<a;
display1(a);
cout<<a;
}
int display1(int &x)
{
x=6;
}

输出

