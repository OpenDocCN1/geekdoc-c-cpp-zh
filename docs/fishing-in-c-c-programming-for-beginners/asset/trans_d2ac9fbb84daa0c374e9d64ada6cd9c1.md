

}
return 0;
}
```

输出

12

continue 语句将控制权放在 for 循环的自增语句处，即 for 循环的第三条语句。因此，i 永远不会被显示，始终显示存储在 i 中的值。

请参考以下程序

```cpp
#include<iostream>
using namespace std;
int main()
{
    int i=1;
    do
    {
    cout<<i;
    continue;
    i++;
    }while(i<5);
}
```

上述代码的输出将是：

![](img/5340985153962870d4e4a3b9453b9146_73_0.png)

即无限次输出 1。因为，就在 cout<<i 之后存在一个 continue 语句，它将控制权放到循环内的第一条语句，即 cout<<i；因此，程序永远不会到达 while 语句，也永远不会终止。

那么下面这段代码呢：

```cpp
#include<iostream>
using namespace std;
int main()
{
    int i=1;
    while(i<5)
    {
    i=10;
    cout<<i;
    continue;
    i++;
    }
}
```
输出
10

这个程序的解答将消除你的疑虑：在 continue 语句之后，控制权是转到 while(i<5) 还是转到 i=10。这意味着 continue; 语句将控制权放在条件处，而不是 while 循环内的第一条语句处。

请参考以下程序

```cpp
#include<iostream>
using namespace std;
int main()
{
    int num=5;
    switch (num)
    {
        case 1: cout<<"1";
        case 5: cout<<"5";
            continue;
        case 6: cout<<"6";
    }
}
```

在这个程序中，你将看到编译错误“continue without a loop”。这是因为 continue 只能在循环中使用。而 break 只能在循环和 switch case 中使用。请参考以下源代码

```cpp
#include<iostream>
using namespace std;
int main()
{
    int num=5;
    break;
    cout<<"Now I am executed";
}
```

这个程序将生成错误“Break statement not within loop or switch”

## 函数

函数是用于执行特定任务的一组语句块。一个值得注意的事实是：“除了 main() 函数外，执行任务根本不需要任何函数”。main() 函数之所以需要，是因为程序执行会查找此函数，如果未定义则会显示编译错误。

尽管如此，我们出于以下原因使用各种函数：

- 1. 通过将任务分为各个部分，使我们的任务更简单。
- 2. 程序易于阅读和理解。
- 3. 更容易纠正错误
- 4. 一个函数中的错误不会影响其他函数。
- 5. 它与给定输入的数值无关

函数有两种类型：

- 1. 库函数：这些在头文件中预定义。
- 2. 用户定义函数：这些是由程序员定义的函数。

函数定义的语法是：

```cpp
return_type func_name(data_type1 arg1,data_type2 arg2,....)
{

/*Statements*/

}
```

其中 arg1、arg2 等称为参数。这些是传递给函数以供进一步处理的参数。

我们到目前为止使用过的一个函数是：

```cpp
int add(int a,int b)
{
return a+b;
}
```

请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int add(int a,int b)
{
    return a+b;
}
int main()
{
    int x=5,y=6;
    cout<<add(x,y);
}
```

输出

11

在这里，我们使用了一个函数 add(int,int)；请看，我们在 main() 函数上方定义了一个函数。很多时候，需要在 main 函数下方定义函数，因此首先我们声明函数，相应的表达式称为函数原型。

函数原型可以以两种方式声明：

第一种方法是：

```cpp
return_type function_name(data_type1,data_type2,...);
```

另一种是：

```cpp
return_type function_name(data_type1 arg1,data_type2 arg2,...);
```

例如，我们使用过的上面的程序也可以以以下方式编写：

```cpp
#include<iostream>
int add(int,int); //This is a function prototype
using namespace std;
int main()
{
    int x=5,y=6;
    cout<<add(x,y);
}
int add(int a,int b)
{
    return a+b;
}
```

输出
11

我们还可以将函数返回的值保存在变量中。
例如，请参考以下程序：

```cpp
#include<iostream>
int power(int,int);
using namespace std;
int main()
{
    int x=5,y=6;
    int c=power(x,y);
    cout<<c;
}
int power(int a,int b)
{
    int temp=1;
    for(int i=0;i<b;i++)
        temp*=a;
    return temp;
}
```

输出
15625

这个程序简单地计算 5 的 6 次幂的值。

## void

很多时候我们不想返回任何东西，在这种情况下我们使用 void 作为返回类型。例如，请参考以下程序：

```cpp
#include<iostream>
using namespace std;
void show_prime_status(int);
int main()
{
    int a;
    cout<<"Enter a number\n";
    cin>>a;
    show_prime_status(a);
}
void show_prime_status(int x)
{
    int i;
    for(i=2;i<x;i++)
    if(x%i==0)
    break;
    if(i==x)
    cout<<x<<" is prime";
    else
    cout<<x<<" is not prime";
}
```

输出

请输入一个数字

12 不是质数

这里，由于我们没有要返回的内容，所以使用了 void 作为返回类型。

请参考以下程序：

```cpp
#include<iostream>
using namespace std;
void welcome();
void bye(void);
int main()
{
    welcome();
    bye();
}
void welcome()
{
    cout<<"Welcome\n";
}
void bye()
{
    cout<<"Bye";
}
```

输出：

欢迎

再见

## 递归

递归是一种调用函数的方法，其中函数从自身内部调用自身。它使程序优雅、吸引人且简洁。但是，它在一定程度上会使程序变慢，因为 C++ 在调用函数时维护一个栈。

请参考以下程序：

```cpp
#include<iostream>
using namespace std;
int factorial(int);
int main()
{
    int a=5;
    cout<<factorial(a);
}
int factorial(int x)
{
    if(x==1 || x==0)
        return 1;
    else
        return x*factorial(x-1);
}
```

输出将是 120。这里，请看在 factorial 函数的定义内部，我们又调用了 (x-1) 的阶乘。该程序将按以下序列执行：

- 5*(5-1)
- 5*((5-1)*(5-2))
- 5*((5-1)*((5-2)*(5-3)))
- 5*((5-1)*((5-2)*((5-3)*(5-4))))
- 5*((5-1)*((5-2)*((5-3)*1)))
- =120

## 变量再探

最初，我们谈论过变量，但没有谈论基于可访问性的变量类型。嗯，基于可访问性，变量分为四种类型：

- 1. 自动存储类
- 2. 静态存储类
- 3. 寄存器存储类
- 4. 外部存储类

Auto – 它是函数内部所有变量的默认数据类型，因此我们在任何地方都没有写 auto。

e.g. auto int a=5;

默认初始值 – 一个不可预测的值，通常称为垃圾值。
生命周期 – 直到控制权停留在定义变量的块中。
作用域 – 局限于定义变量的块。
存储 – 内存。

Static – 静态变量的特性在于它记住最后存储的值。

请参考以下程序

```cpp
#include<iostream>
using namespace std;
void change();
int main()
{
    change();
    change();
}
void change()
{
    static int a=0;
    a++;
    cout<<a;
}
```

这个程序将显示 12。这表明最初 a 的值从 0 增加到 1。现在，当函数第二次被调用时，其值从 1 增加到 2。

Register – 寄存器是一种变量类型，它向编译器请求将变量存储在 CPU 寄存器中（如果可能）；否则它被声明为 auto。寄存器提供对变量的更快读写访问。

在 C++ 中将变量声明为 register，只需在声明前添加 register 关键字。

E.g.

```cpp
register int a=5;
```

- 默认初始值 . 垃圾值。
- 生命周期 . 直到控制权停留在定义变量的块中。
- 作用域 . 局限于定义变量的块。
- 存储 . CPU 寄存器。

Extern – 该变量定义在 main() 和所有其他函数之外。它的值可以被任何函数修改。

请参考以下程序

```cpp
#include<iostream>
using namespace std;
int a=5;
int display1();
int main()
{
    cout<<a;
    display1();
    cout<<a;
}
int display1()
{
    a=6;
}
```

其输出将是 56，因为最初它被赋值为 5，然后调用 display1() 函数，该函数修改其值并将其赋为 6。现在，在函数调用后，控制权返回到 main 函数。现在，在那里显示值时，它显示 6。这里，a 被称为全局变量，可被程序内的所有函数访问。

请参考以下程序：

```cpp
#include<iostream>
```

