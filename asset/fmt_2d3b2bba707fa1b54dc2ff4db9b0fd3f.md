
```cpp
case 12:
    gamestatus=2; // 点数为 2、3 或 12 时玩家输
    break;
default:
    mypoint=sum; // 记录记录点数
    break;
}
while(gamestatus==0)
{
    sum=rolldice(); // 继续掷骰子
    if(sum==mypoint)
    {
        gamestatus=1; // 点数等于记录点数时玩家胜
    }
    else if(sum==7)
    {
        gamestatus=2; // 点数为 7 时玩家输
    }
    // 否则进入下一回合
}
if(gamestatus==1)
    cout<<"player wins"<<endl;
else if(gamestatus==2)
    cout<<"player loses"<<endl;
return 0;
}
int rolldice(void)
{
    int die1,die2,worksum;
    die1=1+rand()%6;
    die2=1+rand()%6;
    worksum=die1+die2;
    cout<<"player rolled "<<die1<<"++"<<die2<<'='<<worksum<<endl;
    return worksum;
}
```

# 3.1 函数的定义与使用

![](img/5618306d085ac1bac8275d6c4c5bbf2a_106_0.png)

**图 3.1:** 函数调用和返回的过程。

被存储，跳转回返回地址并继续执行。图 3.1 显示了调用函数并返回的过程。图中的标签表示了执行顺序。

## 3. 嵌套函数调用

函数内部允许嵌套调用。例如，函数 `A` 调用函数 `B`，然后函数 `B` 调用函数 `C`，这就形成了一个嵌套调用。

**示例 3.7：** 输入整数并计算它们的平方和。

分析：虽然问题很简单，但我们设计了两个函数来展示嵌套调用的工作原理：名为 `fun1` 的函数用于计算平方和，名为 `fun2` 的函数用于计算整数的平方。主函数调用 `fun1`，而 `fun1` 再调用 `fun2`。

源代码：

```cpp
// 3_7.cpp
#include <iostream>
using namespace std;
int main()
{
    int a,b;
    int fun1(int x, int y);
    cin>>a>>b;
    cout<<"Sum of squares of a and b:"<<fun1(a,b)<<endl;
}
int fun1(int x,int y)
{
    int fun2(int m);
    return (fun2(x)+fun2(y));
}
```

## 3. 函数

![](img/5618306d085ac1bac8275d6c4c5bbf2a_107_0.png)

```cpp
int fun2(int m)
{
    return (m*m);
}
```

运行结果：
```
3 4
Sum of squares of a and b:25
```

图 3.2 显示了示例 3.7 中函数调用的顺序。图中的标签表示执行顺序。

## 4. 递归调用

函数可以直接或间接地调用自己。这种函数调用被称为递归调用。

直接调用自己意味着函数体内部包含对自身的函数调用，例如：

```cpp
void fun1(void)
{
    fun1(); // fun1 内部对自身的调用
    ...
}
```

这里是另一个函数间接调用自己的示例：

```cpp
void fun1(void)
{
    fun2();
    ...
}
void fun2(void)
{}
```

```cpp
...
fun1 ();
...
}
```

这里 `fun1` 调用 `fun2`，而 `fun2` 反过来调用 `fun1`。这两个调用构成了间接递归调用。

递归的本质是将原问题分解为一个新问题，而新问题可能会使用原问题的解决方案。按照这一原则继续分解，每个出现的新问题都是原问题的简化子集。最终分解出的问题应该是其解决方案已经已知的。上述过程是有限递归调用。只有有限的递归调用才有意义；无限递归调用将得不到任何结果，没有任何意义。

递归调用的过程由两部分组成：

**第一阶段：递归展开。** 将原问题不断分解为子问题，直到达到已知情况，此时递归结束。例如，我们可以进行如下分解：

`5! = 5 × 4! → 4! = 4 × 3! → 3! = 3 × 2! → 2! = 2 × 1! → 1! = 1 × 0 → 0! = 1`

未知 ←

**第二阶段：回归。** 从已知情况开始，使用分解问题的结果来解决上一个（更复杂的）问题。按照递归的反序逐步重复，直到回到递归的起点。此时回归结束，整个递归完成。计算 `5!` 的回归过程是：

`5! = 5 × 4! = 120 ← 4! = 4 × 3! = 24 ← 3! = 3 × 2! = 6 ← 2! = 2 × 1! = 2 ← 1! = 1 × 0 = 1 ←`

**示例 3.8：** 计算 `n!`

分析：计算 `n!` 的公式为：

`n! = n × (n-1)! if n > 0`
`0! = 1`

该公式是递归的，通过另一个阶乘来计算阶乘。递归的结束条件是 `n=0`。源代码：

```cpp
//3_8.cpp
#include <iostream>
using namespace std;
long fac(int n)
{
  long f;
  if (n==0) f=1;
  else if (n==1) f=1;
  else f=n*fac(n-1);
  return(f);
}
int main()
{
  int n;
  long y;
  cout<<"Enter a positive integer:";
  cin>>n;
  y=fac(n);
  cout<<"\n!="<<y;
}
```

运行结果：

| Enter a positive integer: | n! = |
| :--- | :--- |
| 8 | 40320 |

**示例 3.9：** 从 `n` 中选择 `k` 个元素的组合数（组合数）。

分析：从 `n` 中选择 `k` 个元素的组合数由于公式是递归的，很容易编写一个递归函数来实现计算。递归的结束条件是 `n=k`，此时组合数为 1。然后开始回归。源代码：

```cpp
//3_9.cpp
#include<iostream>
using namespace std;
int main()
{
  int n,k;
  int comm(int n, int k);
  cin>>n>>k;
  cout<<comm(n,k) << endl;
}
int comm(int n, int k)
{
  if ( k>n )
    return 0;
  else if( n==k )
    return 1;
  else
    return comm(n-1,k)+comm(n-1,k-1);
}
```

运行结果：

| 8 5 | 56 |

**示例 3.10：** 汉诺塔游戏。

有三个柱 `A`、`B`、`C`。`N` 个不同大小的盘堆在 `A` 上，大盘在小盘下面，如图 3.3 所示。游戏的过程是将盘从 `A` 移动到 `C`。玩家在游戏可以使用柱 `B`，尽管每次只能移动一个盘，且大盘始终在小盘下面。

分析：将 `n` 个盘从 `A` 移动到 `C` 的过程分为三个步骤：

- 将 `n-1` 个盘从 `A` 移动到 `B`；
- 将 `A` 上的最后一个盘移动到 `C`；
- 将 `n-1` 个盘从 `B` 移动到 `C`；

实际上，这三个步骤包含了两种操作：

- 将多个盘从一个柱移动到另一个柱。这是一个递归操作。
- 将一个盘从一个柱移动到另一个柱。

以下程序使用两个函数来实现上述两种操作 - 第种操作使用 `hanoi` 函数，第二种操作使用 `move` 函数。

![](img/5618306d085ac1bac8275d6c4c5bbf2a_110_0.png)

```cpp
//3_10.cpp
#include <iostream>
using namespace std;
void move(char getone, char putone)
{
    cout << getone << "--" << putone << endl;
}
void hanoi(int n, char getone, char two, char three)
{
    move(getone,putone);
    if (n==1) move(getone,three); // 注意：OCR 为 'one'，上下文暗示为 'getone'
    else
    {
        hanoi(n-1,three,two);
        move(getone,three);
        hanoi(n-1,two,getone,three);
    }
}
int main()
{
    int m;
    cout<<"Enter the number of discs:";
    cin>>m;
    cout<<"the steps to moving """<<m<<" discs:"<<endl;
    hanoi(m,'A','B','C');
}
```

运行结果：
```
Enter the number of discs:3
the steps to moving 3 discs:
A-->C
A-->B
C-->B
A-->C
B-->A
B-->C
A-->C
```

### 3.1.3 函数间的参数传递

在调用函数之前，该函数的形式参数既不占用任何实际内存空间也没有实际值。当进行函数调用时，计算机为形式参数分配内存，并将实参数赋值给形式参数。实参数可以是常量、变量或表达式，并且应该与相应形式参数的类型匹配（参数列表中相同位置的参数）。函数间的参数传递是将形式参数赋值给实参数的过程。C++ 有两种传递参数的方式：值传递和引用传递。

- 1. 值传递

值传递的过程由两个步骤组成：为形式参数分配内存空间，并使用实参数初始化形式参数（将实参数赋值给形式参数）。该过程将实参数的值传递给形式参数。一旦初始化完成，形式参数与实参数之间没有任何关系，之后对形式参数的任何修改都不会影响实参数。

在主函数中执行函数调用：
`Swap(x,y)`

在函数 `Swap` 内部：

| t=a; | | b=t; |
|---|---|------|
| 5 | 10 | 5 | 10 |
| x | y | x | y |

| 5 | 10 | | 5 | 10 |
|---|---|---|---|--|
| a | b | | a | b |
| t | 5 | | t | 5 |

返回到主函数：
`x y`

**图 3.4：** 示例 3.11 中程序运行时的变量状态。

# 运行结果：

```
x=5 y=10
x=5 y=10
```

分析：从运行结果可以看出，变量 `x` 和 `y` 的值没有发生交换。这是因为上面的函数调用使用了**值传递（Call-by-Value）**来传递参数，仅将实参数的值传递给形参数。因此，随后形参数的变化不会影响实参数。图 3.4 显示了程序运行时的变量状态。

### 2. 引用传递（Call-by-Reference）

我们已经看到通过值传递参数是单向的。那么，被调用函数中对形参数的修改如何影响调用函数中的实参数呢？我们可以使用引用传递（Call-by-Reference）来实现这一点。

引用是一种特殊的变量类型；它可以被视为另一个变量的别名。访问变量的引用等同于访问变量本身。这是一个示例：

## 3.1 函数的定义与使用 — 97

```cpp
int i,j;
int &ri=i; // 为 ri 创建一个 int 类型引用，并初始化为 i 的别名
```

```cpp
j=10;
ri=j; // 等同于 i=j;
```

在声明引用现有对象时，必须遵循以下规则：

- 引用必须初始化以指向该对象
- 引用一旦初始化，就不能再更改为指向其他对象。

上述规则表明，引用在整个生命周期内（从定义到结束）应该固定指向某一个对象。

形参数也可以是引用。当形参数为引用时，情况会略有不同：引用类型的形参数在函数类型声明期间不初始化，只有在调用函数时，计算机才会为形参数分配内存空间并将其初始化为实参数。这样，引用类型的形参数就变成了实参数的别名，对形参数的所有操作都会直接影响实参数。

使用引用作为形参数的函数称为引用传递（Call-by-Reference）。

**示例 3.12：** 重写示例 3.11 的程序，使用引用传递使两个整数正确交换。

```cpp
//3_12.cpp
#include<iostream>
using namespace std;
void Swap(int& a, int& b);
int main() {
    int x(5), y(10);
    cout<<"x="<<x<<",y="<<y<<endl;
    Swap(x,y);
    cout<<"x="<<x<<",y="<<y<<endl;
}
```

```cpp
void Swap(int& a, int& b) {
    int t;
    t=a;
    a=b;
    b=t;
}
```

在主函数中执行函数调用：
`Swap(x,y);`

![](img/5618306d085ac1bac8275d6c4c5bbf2a_115_0.png)

在函数 `Swap` 内部：
`t=a; a=b; b=t;`

![](img/5618306d085ac1bac8275d6c4c5bbf2a_115_1.png)

返回到主函数：

图 3.5：示例 3.12 中程序运行时的变量状态。

运行结果：

| x=5 y=10 |
| x=10 y=5 |

分析：从运行结果可以看出，当程序使用引用传递传递参数时，交换是成功的。值传递和引用传递之间的唯一区别在于形参数的声明，而调用函数中的函数调用是相同的。图 3.5 显示了程序运行时的变量状态。

示例 3.13：引用传递的一个示例。

```cpp
//3_13.cpp
#include <iostream>
#include <iomanip>
using namespace std;
void fiddle(int in1, int &in2)
int main()
{
    int count = 7, index = 12;
```

## 3.2 内联函数（Inline Functions） — 99

```cpp
cout << "The values are "; cout<<setw(5)<<count;
cout<<setw(5)<<index<<endl;
fiddle(count, index);
cout << "The values are "; cout<<setw(5)<<count;
cout<<setw(5)<<index<<endl;
```

```cpp
void fiddle(int in1, int &in2)
{
    in1 = 10;
    in2 = 20;
}
```

运行结果：

| The values are | 7 |
| The values are | 12 |
| The values are | 10 |
| The values are | 20 |

分析：第一个参数 `in1` 是值传递的，因此它的值不会改变。第二个参数 `in2` 是引用传递的，因此函数内部的变化会影响实际变量。

内联函数是一种编译器用实际代码替换函数调用的函数。这可以减少调用的开销，但可能会增加二进制代码的大小。

**示例 3.14：** 一个内联函数。

```cpp
inline int square(int x) {
    return x * x;
}
int main() {
    int a = 5;
    cout << square(a) << endl;
    return 0;
}
```

内联函数对于频繁调用的小型函数有用。然而，`inline` 关键字的使用是对编译器的一种建议，编译器可能会选择不内联该函数。

## 3.3 函数中的默认参数

默认参数允许你在函数声明中为参数提供默认值。如果在调用函数时未提供相应的实参数，则使用默认值。

```cpp
void func(int a, int b = 10, int c = 20) {
    cout << a << " " << b << " " << c << endl;
}
int main() {
    func(1); // 输出: 1 10 20
    func(1, 2); // 输出: 1 2 20
    func(1, 2, 3); // 输出: 1 2 3
    return 0;
}
```

默认参数必须从右向左声明。带有值的形参数不应该出现在任何带有默认值的形参数的左侧。

```cpp
void func(int a, int b=5, int c=6); // 正确
void func(int a=1, int b=5, int c); // 错误
void func(int a=1, int b, int c=6); // 错误
```

## 102 — 3 函数

```cpp
int main()
{ add();
}
int add(int x,int y)
{ return x+y;
}
```
