
## 示例

inline double cube(double a)
{
    return(a*a*a);
}

上述内联函数可以通过如下语句调用：

c - cube(3.0);
d - cube(2.5+1.5);

执行这些语句后，c和d的值将分别为27和64。如果参数是诸如此类的表达式 2.5 + 1.5，函数会传递表达式的值，此处即4。这使得内联特性远比宏优越。

将一个函数设为内联函数很容易。我们只需在函数定义前加上关键字 inline。所有内联函数都必须在被调用之前定义。

在将函数设为内联之前，我们应当谨慎。内联函数的速度优势会随着函数规模的增大而减弱。在某一时刻，函数调用的开销相对于函数本身的执行来说变得很小，内联函数的优势可能会丧失。在这种情况下，使用普通函数会更有意义。通常，当函数足够小、能够用一两行代码定义时，才会将其设为内联。例如：

inline double cube(double a) {return(a*a*a);}

请记住，inline 关键字只是向编译器发送一个请求，而不是命令。如果函数定义太长或太复杂，编译器可能会忽略这个请求，并将该函数作为普通函数编译。

以下是一些内联展开可能无法工作的情况：

[PAGE 150]

+   1. 对于有返回值的函数，如果存在循环、switch或goto语句。
+   2. 对于无返回值的函数，如果存在return语句。
+   3. 如果函数包含静态变量。
+   4. 如果内联函数是递归的。

> 注意：*内联*展开使程序运行更快，因为消除了函数调用和返回的开销。然而，它会使程序占用更多内存，因为定义内联函数的语句会在函数被调用的每个地方被复制。因此，有必要进行权衡。

程序4.1演示了内联函数的用法。

# 程序4.1 内联函数

```
#include <iostream>
using namespace std;

inline float mul(float x, float y)
{
    return(x*y);
}

inline double div(double p, double q)
{
    return(p/q);
}

int main( )
{
    float a - 12.345;
    float b - 9.82;
}
```

[PAGE 151]

```
cout << mul(a,b) << "\n";
cout << div(a,b) << "\n";
return 0;
```

程序4.1的输出将是：

```
121.228
1.25713
```

# 4.7 默认参数

C++ 允许我们在调用函数时不指定其所有参数。在这种情况下，函数会为那些在函数调用中没有匹配参数的参数赋予一个*默认值*。默认值在函数声明时指定。编译器查看原型，了解函数使用了多少个参数，并提醒程序可能存在的默认值。以下是一个带有默认值的原型（即函数声明）示例：

float amount(float principal,int period,float rate-0.15);

默认值的指定方式在语法上类似于变量初始化。上述原型为参数 rate 声明了一个默认值 0.15。接下来类似这样的函数调用：

```
value - amount(5000,7);    // one argument missing
```

将 5000 传递给 principal，7 传递给 period，然后让函数对 rate 使用默认值 0.15。调用

```
value - amount(5000,5,0.12);       // no missing argument
```

将显式值 0.12 传递给 rate。

[PAGE 152]

默认参数在声明时进行类型检查，在调用时进行求值。需要注意的重要一点是，只有尾随的参数才能有默认值，因此我们必须从*从右到左*添加默认值。我们不能为参数列表中间的某个参数提供默认值。以下是一些带有默认值的函数声明示例：

默认参数在有些参数总是具有相同值的情况下很有用。例如，在特定的存款期限内，银行利率对所有客户可能保持不变。它还为程序员提供了更大的灵活性。一个函数可以写成包含比其最常见应用所需的更多参数。使用默认参数，程序员可以只使用对特定情况有意义的那些参数。程序4.2演示了默认参数的用法。

# 程序4.2 默认参数

```
#include<iostream>
#include<conio.h>

using namespace std;

int main( )
{
    float amount;
    float value(float p, int n, float r-0.15); //prototype
    void println(char ch-‘*’,int len-40); //prototype
    println();
    //use default values for arguments
```

[PAGE 153]

```cpp
amount - value (5000.00,5);        //default for 3rd argument
cout<<"\n Final Value - "<<amount<<"\n\n";

amount - value (10000.00,5,0.30); //pass all arguments explicitly

cout<<"\n Final Value - "<<amount<<"\n\n";

printline('-');                    //use default value for second argument

getch ( );

return 0;
}
float value (float p, int n, float r)
{
    int year - 1; float sum - p;

    while(year<-n)
    {
        sum - sum*(1+r);
        year - year+1;
    }
    return (sum);
}
void printline(char ch, int len)
{
    for (int i-1;i<=len;i++)
        printf("%c",ch);
    printf("\n");
}
```

程序4.2的输出将是：

[PAGE 154]

```
**********************************
Final Value - 10056.8
Final Value - 37129.3
----------------------------------
```

提供默认参数的好处有：

+   1. 我们可以使用默认参数为现有函数添加新参数。
+   2. 默认参数可用于将相似函数合并为一个。

# 4.8 const 参数

在C++中，函数的参数可以声明为 const，如下所示。

int strlen(const char *p);
int length(const string &s);

限定符 **const** 告诉编译器，函数不应修改该参数。当此条件被违反时，编译器将生成错误。这种声明仅在按引用或指针传递参数时才有意义。

# 4.9 递归

递归是一种函数调用自身的情况，也就是说，函数定义中的某条语句调用了它所在的同一个函数。这听起来可能像一个无限循环条件，但正如循环有条件检查来使程序控制退出循环一样，递归函数也拥有一个基准情况，它将程序控制从当前函数实例返回到调用函数。例如

[PAGE 155]

例如，在一系列计算某个数阶乘的递归调用中，基准情况将是计算0的阶乘的情况。让我们考虑几个示例（程序4.3和4.4）来理解递归方法的工作原理。

# 程序4.3 —— 计算一个数的阶乘

```cpp
#include <iostream>
#include <conio.h> using namespace std;

long fact(int n)
{
    if (n -- 0)       //base case
        return 1;

    return (n * fact(n-1));     //recursive function call
}
int main( )
{
    int num;

    cout << “Enter a positive integer: “;
    cin >> num;

    cout << “Factorial of “ << num << “ is “ << fact(num);

    getch( );
    return 0;
}
```

程序4.3的输出将是：

[PAGE 156]

Enter a positive integer: 10
Factorial of 10 is 3628800

# **程序4.5** 解决汉诺塔问题

```cpp
#include <iostream>
#include <conio.h>
using namespace std;

void TOH(int d,char tower1, char tower2, char tower3)
{
    if (d-1) //base case
    {
        cout << "\nShift top disk from tower " << tower1 << " to tower " << tower2;
        return;
    }
    TOH(d-1,tower1, tower3, tower2); //recursive function call
    cout << "\nShift top disk from tower " << tower1 << " to tower " << tower2;
    TOH(d-1,tower3, tower2, tower1); //recursive function call
}
int main()
{
    int disk;

    cout << "Enter the number of disks: ";
    cin >> disk;

    if (disk < 1)
        cout << "\nThere are no disks to shift";
    else
        cout <<"\nThere are " << disk << " disks in tower 1\n";
}
```
