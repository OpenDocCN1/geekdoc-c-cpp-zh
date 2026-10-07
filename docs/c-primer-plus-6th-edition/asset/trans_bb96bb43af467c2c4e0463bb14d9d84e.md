

# 910 第15章 友元、异常及其他

```
int main() {
  ...
  try {
    afunct();
    nextfunc();
  }
  catch(const char * s) {
    ...
  }
}
```

```
void afunct(); {
  ...
  bfunct();
  return;
...}
```

```
void bfunct(); {
  ...
  cfunct();
  return;
...}
```

```
void cfunct(); {
  ...
  if(oops) throw "Help!";
  return;
...}
```

使用 return

```
int main() {
  ...
  try {
    afunct();
    nextfunc();
  }
  catch(const char * s) {
    ...
  }
}
```

```
void afunct(); {
  ...
  bfunct();
  return;
...}
```

```
void bfunct(); {
  ...
  cfunct();
  return;
...}
```

```
void cfunct(); {
  ...
  if(oops) throw "Help!";
  return;
...}
```

使用 throw

图 15.3 throw 与 return 的对比。

在代码响应并显示消息后，它会重新抛出异常，这意味着，在这种情况下，将异常发送到 main()。 （一般来说，重新抛出的异常会上升到捕获该特定类型异常的下一个 try-catch 组合。如果找不到处理程序，则默认情况下会中止。）列表 15.12 使用了列表 15.10 中的相同处理程序文件 exc_mean.h 作为列表 15.11。

列表 15.12 error5.cpp

```
//error5.cpp -- unwinding the stack
#include <iostream>
#include <cmath> // math.h, unix users may need -lm flag
#include <string>
#include "exc_mean.h"
```

```
class demo {
private:
  std::string word;
public:
  demo (const std::string & str
{
    word = str;
    std::cout << "demo" << word << " created\n";
}
~demo()
{
    std::cout << "demo" << word << " destroyed\n";
}
void hmean() const
{
    std::cout << "demo" << word << " lives!\n";
}
;
```

```
// function prototypes
double hmean(double a, double b);
double gmean(double a, double b);
double means(double a, double b);
```

```
int main(){
    using std::cout;
    using std::cin;
    using std::endl;

double x, y, z;
{
    demo d1("found in block in main()");
    cout << "Enter two numbers: ";
    while (cin >> x >> y) {
        try { // start of try block
            z = means(x,y);
            cout << "The mean of " << x << " and " << z << std::endl;
            cout << "Enter next pair: ";
        } // end of try block
        catch (bad_hmean & bg) { // start of catch block
            bg.mesg();
            cout << "Try again.\n";
            continue;
        } catch (bad_gmean & h) {
            cout << h.mesg();
```

```
cout << "Values used: " << hg.v1 << "",
<< hg.v2 << endl;

cout << "Sorry, you don't get to play any more.\n"
break;
} // end of catch block
}
d1.show();
}
cout << "Bye!\n";
cin.get();
cin.get();
return 0;
```

```
double hmean(double a, double b)
{
    if (a == -b)
        throw bad_hmean(a,b);
    return 2.0 * a * b / (a + b);
}
```

```
double gmean(double a, double b)
{
    if (a < 0 || b < 0)
        throw bad_gmean(a, b);
    return std::sqrt(a * b);
}
```

```
double means(double a, double b)
{
    double am, hm, gm;
demo d2("found in means()");
am = (a + b) / 2.0; // arithmetic mean
try{
    hm = hmean(a,b);
    gm = gmean(a,b);
} catch (bad_hmean & bg) // start of catch block{
    bg.msg2();
    std::cout << "Caught in means()\n";
    throw; // rethrows the exception
}
d2.show();
return (am + hm + gm) / 3.0;
}
```

# 异常 913

以下是该程序的一个示例运行：

```
demo found in block in main() created
Enter two numbers: 6 12
demo found in means() created
demo found in means() lives!
demo found in means() destroyed
The The mean of 6 and 12 is 849509
6 -6
demo found in means() created
mean(6, -6): invalid arguments: a = -b
Caught in means()
demo found in means() destroyed
mean(6, -6): invalid arguments: a = -b
Try again.
6 -8
demo found in means() created
demo found in means() destroyed
gmean() arguments should be 0
Values used: 6, -8
Sorry, you don’t get to play any more.
demo found in block in main() lives!
demo found in block in main() destroyed
Bye!
```

# 程序说明

让我们追踪前一节所示的示例运行过程。首先，正如 demo 构造函数所宣布的那样，一个对象在 main() 中的块中被创建。接下来，调用 means()，并创建另一个 demo 对象。means() 函数将值 6 和 12 传递给 hmean() 和 gmean()，这些函数将返回值给 means()，后者计算结果并返回它。在返回结果之前，means() 调用 d2.show()。返回结果后，means() 终止，并且 d2 的析构函数会自动调用：

```
demo found in means() lives!
demo found in means() destroyed
```

下一个输入周期将值 6 和 -6 发送到 means()，然后 means() 创建一个新的 demo 对象并将值传递给 hmean()。hmean() 函数抛出一个 bad_hmean 异常，该异常被 means() 中的 catch 块捕获，如以下输出所示：

```
mean(6, -6): invalid arguments: a = -b
Caught in means()
```

# 第15章 友元、异常及其他

此代码中的 throw 语句开始，当它终止 means() 并将异常发送到 main() 时。事实证明 d2.show() 未被调用，这证明了 means() 的执行被终止。但请注意，d2 的析构函数被调用：

demo found in means() destroyed

这说明了异常的一个极其重要的方面：随着程序展开堆栈以到达捕获异常的位置，它会释放堆栈上的自动存储类变量。如果某个变量恰好是一个类对象，则会调用该对象的析构函数：

与此同时，被抛出的异常捕获 main()，其中适当的 catch 块捕获并处理它

```
hmean(6, -6) : invalid arguments: a = -b
Try again.
```

现在第三个输入周期开始，将 6 和 -8 发送到 means()。同样，means() 创建了一个新对象。它将 6 和 -8 处理到 hmean()，后者对其进行处理没有问题。然后 means() 将 6 和 -8 传递给 gmean()，后者抛出一个 bad_gmean 异常。因为 means() 不捕获 bad_gmean 异常，所以异常会传递到 main()，并且 means() 中的后续代码不会被执行。然而，再次，随着程序展开堆栈，它会释放本地自动变量，因此 d2 的析构函数被调用：

```
demo found in means() destroyed
```

最后，main() 中的 bad_gmean 处理程序捕获异常并终止循环：

```
gmean() arguments should >= 0
Values used: 6, -8
Sorry, you don't get to play any more.
```

程序正常终止，显示一些消息并自动调用 d1 的析构函数。如果 catch 块使用，例如 exit (EXIT_FAILURE) 而不是 break，程序将立即终止，因此你看不到这些消息：

```
demo found in main() lives!
Bye!
```

但是，你仍然会看到这条消息：
demo found in main() destroyed

再次，异常机制会负责释放堆栈上的自动变量。

# 更多异常特性

尽管 throw-catch 机制与函数参数和函数返回机制相似，但存在一些差异。其中之一，你已经遇到过，即函数 fun() 中的 return 语句将执行转移到调用 fun() 的函数，但 throw 将执行一直转移到第一个具有捕获异常的 try-catch 组合的函数。例如，在列表 15.12 中，当 hmean() 抛出异常时，控制权传递到 means()，但当 gmean() 抛出异常时，控制权传递到 main()。

另一个区别是，编译器在抛出异常时总是创建一个临时副本，即使异常说明符和 catch 块指定引用。在实例中，考虑以下代码：

```
class problem {...};
...
void super() throw (problem)
{
    if (oh_no)
    {
        problem oops; // construct object
        throw oops; // throw it
        ...
    }
}
try {
    super();
}
catch(problem & p)
{
// statements
```

这里，p 将引用 oops 的副本而不是 oops。这是一件好事，因为 super() 终止后 oops 不再存在了。顺便说一下，将构造与 throw 结合起来更简单：

throw object(); // construct and throw default object

此时你可能会想知道为什么代码使用引用，如果 throw 生成副本的话。毕竟，使用返回值的通常原因是避免复制的效率。答案是引用还有另一个重要的属性：基类引用也可以引用派生类对象。假设你有一组通过继承派生的异常类型。在这种情况下，异常说明符只需列出对基类型的引用，这也将匹配任何派生对象。

假设你有一个异常的类层次结构，并且你想分别处理不同的类型。基类引用可以捕获一个家族的所有对象，但派生类对象只能捕获该对象和从该类派生的类的对象。被抛出的对象由第一个匹配它的 catch 块捕获。这表明按派生的逆序排列 catch 块：

