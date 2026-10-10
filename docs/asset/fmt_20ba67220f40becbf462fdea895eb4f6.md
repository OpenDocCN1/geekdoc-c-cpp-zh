
输出

A created
A destroyed
Exception in abc

正如我们看到的，调用 `abc()` 函数后 `main()` 函数的剩余部分没有执行。相反，程序终止了。这是因为对 `abc()` 函数的调用没有放在 `try` 块中。因此，当 `abc()` 函数抛出异常时，应用程序程序员没有指定任何 catch 处理程序来执行期望的代码。程序直接带有默认错误消息终止。

```cpp
catch(hmeanxcp& e)
{
  cout<<e.getError()<<endl;
  cout<<"Enter a fresh pair of numbers\n";
  continue;
}
catch(gmeanxcp& e)
{
  cout<<e.getError()<<endl;
  cout<<"Enter a fresh pair of numbers\n";
  continue;
}
cout<<"Harmonic mean = "<<z1<<endl;
cout<<"Geometric mean = "<<z2<<endl;
cout<<"Enter again ? "<<choice<< (y/n)\n";
cin>>choice;
}
cout<<"Bye\n";
```

```cpp
double hmean(double a,double b)
{
  if(a==-b)
    throw hmeanxcp("Exception error - a=-b not allowed");
  return 2.0*a*b/(a+b);
}
double gmean(double a,double b)
{
  if(a*b<0)
    throw gmeanxcp("Exception error - a*b<0 not allowed");
  return sqrt(a*b);
}
```

# 输出

输入一个数字: 10<enter>
输入另一个数字: -10<enter>
Exception error - a=-b not allowed
Enter a fresh pair of numbers
输入一个数字: 10<enter>
输入另一个数字: -6<enter>
Exception error - a*b<0 not allowed
Enter a fresh pair of numbers
输入一个数字: 16<enter>
输入另一个数字: 4<enter>
Harmonic mean = 6.4
Geometric mean = 8
Enter again? (y/n) n<enter>
Bye

被抛出的对象的临时副本会被创建并被抛出。因此，catch 处理程序中的对象指向的是被抛出对象的副本。这是理想的，因为被抛出的对象在抛出它的函数执行后就会消失。因此，在对象被抛出后，可能会创建它的三个副本——它本身，以及 catch 块中的对象。对象本身会在函数终止时自动销毁。

因此，我们剩下了两个副本。为了将这个数量减少到一个，我们通常会在 catch 处理程序中创建一个指向被抛出对象的引用（如列表 11.10 中的 catch 块所示）。

## 11.3.5 抛出嵌套异常的参数化对象

让我们来看列表 11.11。

列表 11.11 嵌套异常类

```cpp
#include<iostream.h>
#include<string.h>
template<class T>
class vector
{
    T * v;
    int size;
public:
    class RangeError
    {
        char Error[30];
        int errorPos;
        public:
        RangeError(char * str,int p)
        {
            strcpy(Error,str);
            errorPos=p;
        }
        char * getError()
        {
            return Error;
        }
        int getPos()
        {
            return errorPos;
        }
    };
    vector(int s)
    {
        v=new T[s];
        size=s;
    }
    ~vector()
{
        delete[] v;
    }
    void setElement(T val,int p)
    {
        if(p>size-1 || p<0)
            throw RangeError("Out of range exception - could not write",p);
        v[p]=val;
    }
    T& getElement(int p)
    {
        if(p>size-1 || p<0)
            throw RangeError("Out of range exception - could not read",p);
        return v[p];
    }
};
```

```cpp
void main() {
  vector<int> int_vector(5);
  try {
    int_vector.setElement(3,5);
    cout << int_vector.getElement(3) << endl;
  } catch(vector<int>::RangeError& e) {
    cout << e.getError() << " at position " << e.getPos() ++1 << endl;
  }
  vector<float> float_vector(6);
  try {
    float_vector.setElement(3.14,3);
    cout << float_vector.getElement(6) << endl;
  } catch(vector<float>::RangeError& e) {
    cout << e.getError() << " at position " << e.getPos() ++1 << endl;
  }
}
```

# 输出
Out of exception – could not write at position 6
Out of exception – could not read at position 7

我们可以将异常类定义为抛出异常的类的嵌套类。这指示了产生异常的类。它还防止了全局命名空间的污染。在列表 11.11 的示例中，`RangeError` 类已在 `vector` 类内部声明。如果 `setElement()` 函数或 `getElement()` 函数发现错误的下标值，它会抛出一个类型为 `RangeError` 的异常。该异常的处理程序如下：

```cpp
catch(vector<int>::RangeError& e) {...}
```

值得注意的是，嵌套异常类是公共的。这允许 catch 块访问该类型。

## 11.3.6 捕获已捕获异常

C++ 语言支持一种功能，可以捕获在 try 块中抛出但未被任何 catch 块捕获的异常。处理异常的 catch 构造语法如下：

```cpp
catch(...)
```

可以注意的是，`...` 捕获了在 try 块中抛出但未被任何 catch 块捕获的异常。`...` 在 catch 构造中表示它可以捕获所有类型。列表 11.12 展示了这种 catch 的用法。

```cpp
#include<iostream.h>
class Sugar{};
class Spice{};
void abc(int);
void main()
{
    try {
        abc(1);
    } catch(Sugar) {
        cout<<"Caught Sugar\n";
    } catch(Spice) {
        cout<<"Caught Spice\n";
    } catch(...) {
        cout<<"Caught unknown\n";
    }
}
void abc(int p)
{
    if(p==1)
        throw Sugar();
    if(p==2)
        throw Spice();
    else
        throw 123;
}
```

```cpp
void func(int p) {
    try {
        abc(p);
    } catch(...) {
        throw;
    }
}
```

# 输出
Caught Sugar
Caught Spice
Caught unknown

捕获已捕获的异常

C++ 语言支持一种功能，可以捕获在 try 块中抛出但未被任何 catch 块捕获的异常。处理异常的 catch 构造语法如下：

```cpp
catch(...)
```

`...` 在 catch 构造中表示它可以捕获所有类型。列表 11.12 展示了这种 catch 的用法。
