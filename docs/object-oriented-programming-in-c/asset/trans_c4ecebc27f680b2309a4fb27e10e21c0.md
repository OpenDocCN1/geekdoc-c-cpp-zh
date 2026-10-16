
> note
> 内联展开使程序运行更快，因为函数调用和返回的开销被消除了。然而，它会使程序占用更多内存，因为定义内联函数的语句会在函数被调用的每个位置被复制。因此，需要进行权衡。

程序 4.1 说明了内联函数的使用。

## INLINE FUNCTIONS

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

int main()
{
    float a = 12.345;
    float b = 9.82;

    cout << mul(a,b) << "\n";
    cout << div(a,b) << "\n";

    return 0;
}
```

PROGRAM 4.1

程序 4.1 的输出为

121.228
1.25713

## 4.7 Default Arguments

C++ 允许我们在不指定其所有参数的情况下调用函数。在这种情况下，函数会为在函数调用中没有匹配参数的参数分配默认值。默认值在函数声明时指定。编译器会查看原型以查看函数使用多少个参数，并提醒程序可能存在的默认值。以下是带有默认值的原型（即函数声明）的示例：

```
float amount(float principal,int period,float rate=0.15);
```

默认值以与变量初始化类似的语法指定。上述原型为参数 rate 声明了 0.15 的默认值。随后类似的函数调用

```
value = amount(5000,7);      // 缺少一个参数
```

将值 5000 传递给 principal，7 传递给 period，然后让函数对 rate 使用默认值 0.15。调用

```
value = amount(5000,5,0.12);      // 没有缺少的参数
```

将显式值 0.12 传递给 rate。

默认参数在声明时检查类型，在调用时求值。需要注意的一个重要点是，只有尾部参数可以有默认值，因此我们必须从右到左添加默认值。我们不能为参数列表中间的某个特定参数提供默认值。以下是带有默认值的函数声明的一些示例：

```
int mul(int i, int j=5, int k=10);      // 合法
int mul(int i=5, int j);                // 非法
int mul(int i=0, int j, int k=10);      // 非法
int mul(int i=2, int j=5, int k=10);    // 合法
```

在某些参数始终具有相同值的情况下，提供默认参数很有用。例如，银行利息在特定存款期间对所有客户可能保持不变。它还为程序员提供了更大的灵活性。函数可以用比其最常见应用所需的更多的参数编写。使用默认参数，程序员只能使用对特定情况有意义的参数。程序 4.2 说明了默认参数的使用。

## DEFAULT ARGUMENTS

```
#include <iostream>

using namespace std;

int main()
{
    float amount;

    float value(float p, int n, float r=0.15);  // prototype
    void println(char ch='*', int len=40);      // prototype

    println();                  // uses default values for arguments

    amount = value(5000.00,5);          // default for 3rd argument

    cout << "\n      Final Value = " << amount << "\n\n";

    println('=');       // use default value for 2nd argument

    return 0;
}
/*------------------------------------------------------------*/
float value(float p, int n, float r)
{
    int year = 1;
    float sum = p;

    while(year <= n)
    {
        sum = sum*(1+r);
        year = year+1;
    }
    return(sum);
}

void println(char ch, int len)
{
    for(int i=1; i<=len; i++) printf("%c",ch);
    printf("\n");
}
```

程序 4.2 的输出为

```
***********************************

    Final Value = 10056.8

===================================
```

提供默认参数的优点是：

- 1. 我们可以使用默认参数为现有函数添加新参数。
- 2. 默认参数可用于将相似函数合并为一个。

## 4.8 const Arguments

在 C++ 中，函数的参数可以声明为 const，如下所示。

```
int strlen(const char *p);
int length(const string &s);
```

限定符 const 告诉编译器函数不应修改参数。当此条件被违反时，编译器会生成错误。这种类型的声明只有在我们通过引用或指针传递参数时才有意义。

## 4.9 Function Overloading

如前所述，重载是指对不同目的使用同一事物。C++ 也允许函数重载。这意味着我们可以使用相同的函数名创建执行各种不同任务的函数。这在 OOP 中称为函数多态性。

使用函数重载的概念，我们可以用一个函数名设计一组函数，但参数列表不同。函数将根据函数调用中的参数列表执行不同的操作。要调用的正确函数是通过检查参数的数量和类型而不是函数类型来确定的。例如，重载的 add() 函数处理不同类型的数据，如下所示：

```
// Declarations
int add(int a, int b);                      // prototype 1
int add(int a, int b, int c);               // prototype 2
double add(double x, double y);             // prototype 3
double add(int p, double q);                // prototype 4
double add(double p, int q);                // prototype 5

// Function calls
cout << add(5, 10);                         // uses prototype 1
cout << add(15, 10.0);                      // uses prototype 4
cout << add(12.5, 7.5);                     // uses prototype 3
cout << add(5, 10, 15);                     // uses prototype 2
cout << add(0.75, 5);                       // uses prototype 5
```

函数调用首先匹配具有相同数量和类型参数的原型，然后调用适当的函数执行。最佳匹配必须是唯一的。函数选择涉及以下步骤：

- 1. 编译器首先尝试找到完全匹配，其中实际参数的类型相同，并使用该函数。
- 2. 如果找不到完全匹配，编译器会使用对实际参数的整型提升，例如，
- 3. 当两者都失败时，编译器会尝试使用内置转换（隐式赋值转换）对实际参数进行转换，然后使用匹配唯一的函数。如果转换可能产生多个匹配，则编译器会生成错误消息。假设我们使用以下两个函数：
- 4. 如果所有步骤都失败，则编译器会尝试用户定义的转换结合整型提升和内置转换来找到唯一的匹配。用户定义的转换通常用于处理类对象。

```
char to int
float to double
```

```
long square(long n)
double square(double x)
```

函数调用例如

```
square(10)
```

会引起错误，因为 int 参数可以转换为 long 或 double，从而造成应使用 square() 的哪个版本的不明确情况。

程序 4.3 说明了函数重载。

## FUNCTION OVERLOADING

```
// Function volume() is overloaded three times

#include <iostream>

using namespace std;

// Declarations (prototypes)
int volume(int);
double volume(double, int);
long volume(long, int, int);

int main()
{
    cout << volume(10) << "\n";
    cout << volume(2.5,8) << "\n";
    cout << volume(100L,75,15) << "\n";
    return 0;
}

// Function definitions

int volume(int s)  // cube
{
    return(s*s*s);
}

double volume(double r, int h)  // cylinder
{
    return(3.14519*r*r*h);
}

long volume(long l, int b, int h) // rectangular box
{
    return(l*b*h);
}
```

PROGRAM 4.3

程序 4.3 的输出为：

1000
157.26
112500

函数重载应谨慎进行。我们不应重载不相关的函数，而应将函数重载保留给执行密切相关任务的函数。有时，默认参数可代替重载使用。这可减少需要定义的函数数量。

重载函数被广泛用于处理类对象。当在下一章讨论类时，将对其进行说明。

## 4.10 Friend and Virtual Functions

C++ 引入了两种新型函数，即友元函数和虚函数。它们基本上是为了处理与类对象相关的某些特定任务而引入的。因此，对这些函数的讨论已推迟到类对象讨论之后。友元函数在下一章的第 5.15 节中讨论，虚函数在第 9 章的第 9.5 节中讨论。
