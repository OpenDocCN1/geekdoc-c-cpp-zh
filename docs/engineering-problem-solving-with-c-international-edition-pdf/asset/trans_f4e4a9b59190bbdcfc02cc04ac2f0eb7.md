

```cpp
//Get values for a and b.
cout << "Enter two integer values: ";
cin >> a >> b;

//Print values of a and b before the swap
cout << "Before swap:\n a is " << a << " b is " << b << endl;

//Call swap function and print values
swapIntegers(a,b);
cout << "After call to swapIntegers:\n a is " << a
     << " b is " << b << endl;

//Exit main
return 0;
}
```

我们的驱动程序的示例运行产生以下结果：

Enter two integer values: 5 10
Before swap:
a is 5 b is 10
After call to swapIntegers:
a is 10 b is 5

![](img/f2bfa570e453b020c16e048c79a3ea0e_261_0.png)

为进一步说明按引用传递，我们提供了程序执行的跟踪，省略了 cout 语句。请注意，定向箭头用于指示，当使用按引用传递时，形参引用或指向函数实参。

## 程序跟踪

main()
步骤 1: int a, b;
步骤 2: cin >> a >> b;
步骤 3: swapIntegers(a, b);
步骤 8: return 0;

swapIntegers(int a, int b)
步骤 4: integer hold = a;
步骤 5: a = b;
步骤 6: b = hold;
步骤 7: return;

## 内存快照

| 步骤 | main() | swapIntegers(int a, int b) |
|------|--------|----------------------------|
| 步骤 1: | 整数 a ?<br>整数 b ? | |
| 步骤 2: | 整数 a 5<br>整数 b 10 | |
| 步骤 3: | 整数 a [5] <------- [ ] 整数 a<br>整数 b [10] <------ [ ] 整数 b | |
| 步骤 4: | 整数 a [5] <------- [ ] 整数 a<br>整数 b [10] <------ [ ] 整数 b<br>             [5] 整数 hold | |
| 步骤 5: | 整数 a [10] <------ [ ] 整数 a<br>整数 b [10] <------ [ ] 整数 b<br>             [5] 整数 hold | |
| 步骤 6: | 整数 a [10] <------ [ ] 整数 a<br>整数 b [5] <------- [ ] 整数 b<br>             [5] 整数 hold | |
| 步骤 7: | 整数 a [10]<br>整数 b [5]<br>函数变量已释放。 | |
| 步骤 8: | 所有内存已释放。 | |

请记住，函数实参和形参必须在顺序、类型和数量上一致，但名称不必相同。在上面的示例中，我们选择为函数实参和形参使用相同的标识符。这是允许的，因为这些标识符定义在不同的语句块中。然而，重要的是要意识到在 main 函数中定义的 a 和 b 占用的内存位置与在函数头中定义的 a 和 b 不同。与按引用传递参数对应的函数实参必须是变量，因为它们的值可以被修改。常量和表达式不能作为按引用传递参数的实参。

## 修改！

- 1. 修改上一节开发的驱动程序，添加以下函数调用：

```
swapIntegers(10, 5);
```

当您尝试编译和执行程序时，您会看到什么结果？请解释。

## 修改！

2. 修改上一节开发的驱动程序，添加以下函数调用：

```
swapIntegers(a, a * b);
```

当您尝试编译和执行此程序时，您会看到什么结果？请解释。

## 练习！

在第 1–4 题中，考虑对 `swapIntegers` 函数的引用。对于无效引用，解释引用无效的原因。对于有效引用，给出引用前后的内存快照。

- 1. int x=1, y=3;
     ...
     swapIntegers(x,y):

- 2. ...
     swapIntegers(10,5):

- 3. int x=1, y=3;
     ...
     swapIntegers(x, x+y5):

- 4. double x=1.5, y=3.2;
     ...
     swapIntegers(x,y):

- 5. 以下程序输出什么？

```
#include<iostream>
using namespace std;
void fun_ch6(int first, int& second);
int main()
{
    int n1(0), n2(0);
    fun_ch6(n1,n2);
    cout << n1 << endl << n2 << endl;
    return 0;
}
void fun_ch6(int first, int& second)
{
    first++;
    second += 2;
    return;
}
```

## 存储类和作用域

- 作用域
- 存储类
- 局部
- 全局
- 自动存储类
- 外部存储类

在迄今为止介绍的示例程序中，我们在 main 函数和程序员定义的函数内声明了对象，并将函数原型放在 main 函数之前。也可以在 main 函数之前定义对象。这会影响对象的作用域，作用域是指可以引用该对象的程序部分。作用域有时也定义为对象可见或可访问的程序部分。能够确定函数或对象的作用域非常重要。因为对象的作用域与其存储类直接相关，我们还将讨论四种存储类：自动、外部、静态和寄存器。

首先，我们定义局部作用域与全局或文件作用域之间的区别。局部对象在函数内定义，因此包括形参以及函数中声明的任何其他对象。局部对象只能在定义它的函数中访问。局部对象在其函数执行时具有值，但函数完成后其值不会保留。全局对象在 main 函数或其他程序员定义的函数之外定义。全局对象的定义位于所有函数之外，因此可以被程序文件中的任何函数访问。自动存储类用于表示局部对象；这是默认存储类，但也可以在类型说明前使用关键字 auto 来指定。外部存储类用于表示全局对象。

考虑包含以下语句的程序：

```
#include <iostream>
using namespace std;

int count(0);
...
int main()
{
   int x, y, z;
   ...
}
int calc(int a, int b)
{
   int x;
   count += x;
   ...
}
void check(int sum)
{
   count += sum;
   ...
}
```

对象 count 是全局对象，因此可以被函数 calc() 和 check() 引用。对象 x、y 和 z 是局部对象，只能在 main 函数中引用；同样，对象 a、b 和 x 是局部对象，只能在函数 calc() 中引用，sum 是局部对象，只能在函数 check() 中引用。请注意，有两个名为 x 的局部对象——它们是作用域不同的两个不同对象。

分配给全局对象的内存在整个程序运行期间保留。虽然可以从函数引用全局对象，但通常不鼓励使用全局对象。一般来说，更倾向于使用参数向函数传递信息，因为参数在函数原型中很明显，而全局对象在函数原型中不可见。应避免使用非常量全局对象。

函数名也具有外部存储类，因此可以从其他函数引用。任何函数之外的函数原型和 #include 指令也是全局的，因此可供程序中所有其他函数使用；这解释了为什么我们不需要在引用数学函数的每个函数中都包含头文件 cmath。

静态存储类用于指定局部对象的内存应在整个程序执行期间保留。因此，如果在函数中的局部对象在其类型说明前使用关键字 static 赋予静态存储类，则当程序退出定义该对象的函数时，该对象不会丢失其值。静态对象可用于计算函数被调用的次数，因为计数的值会在一次函数调用到下一次调用之间保留。以下程序说明了静态存储类的用法：

```
#include<iostream>
using namespace std;

void ch6_static();

int main()
{
   ch6_static();
   ch6_static();
   ch6_static();
}

void ch6_static()
{
   int x(0);
   static int count(0);
   x++;
   count++;
   cout << x << ", " << count << endl;
   return;
}
```

第一次调用函数 ch6_static() 时，对象 x 和 count 被定义和初始化。由于 count 是静态的并保留其值，在对函数的所有后续调用中都会忽略初始化。该程序的输出如下：

1, 1
1, 2
1, 3

关键字 register 用于对象的类型说明之前，以指定它应放置在寄存器或高速内存位置。访问寄存器比访问内存更快，因此这种存储类用于频繁访问的值。

