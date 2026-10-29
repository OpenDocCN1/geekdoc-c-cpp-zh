

# 模板与继承

你已经在使用基本字符串模板类的一个特例。未修饰的名称 string，我们一直在使用，是类 basic_string<char> 的别名。你为类 string 学到的所有成员函数都适用于模板类 basic_string<>，并且行为相似。

模板类 basic_string 在库中以头文件 <string> 定义，其定义放在 std 命名空间中。因此在使用类 basic_string 时，你需要在文件开头附近写下以下内容或类似内容：

```
#include <string>
using namespace std;
```

或

```
#include <string>
using std::basic_string;
using std::string; //Only if you use the name string by itself
```

> *The ruling ideas of each age have ever been the ideas of its ruling class.*
> 
> — Karl Marx and Friedrich Engels, *The Communist Manifesto*

关于模板和继承几乎没有什么新东西需要学习。要定义一个派生模板类，你从一个模板类（有时是普通类）开始，并从中派生出另一个模板类。你以与从普通基类派生普通类相同的方式来做。示例应能澄清你对语法细节可能有的任何疑问。

# 示例：带备份的部分填充数组的模板类

第 14 章（图 14.10 和 14.11）定义了用于带备份的 double 部分填充数组的类 PFArrayDoub。我们将其定义为 PFArrayD（图 14.8 和 14.9）的派生类。类 PFArrayD 是一个部分填充数组的类，但它仅适用于基类型 double。图 16.5 和 16.6 将类 PFArrayD 转换为模板类 PFArray，使其适用于任何类型作为数组基类型。在本程序中，我们将定义模板类 PFArrayBak，用于带备份的部分填充数组，可适用于任何类型作为数组基类型。我们将模板类 PFArrayBak 定义为模板 PFArray 的派生类。我们可以通过从常规派生类 PFArrayDoub 开始，将所有出现的数组基类型 double 替换为类型参数 T，将类 PFArrayD 替换为模板类 PFArray，并清理语法使其完全符合模板语法，来几乎自动地完成此操作。

模板类 PFArrayBak 的接口在图 16.8 中给出。请注意基类是 PFArray<T> 带有数组参数，而不是简单的 PFArray。如果你想一想，你会意识到你需要 <T>。T 的部分填充数组带备份是 T 的部分填充数组的派生类。T 很重要，它的使用方式也很重要。

模板类 PFArrayBak 的实现在图 16.9 中给出。下面我们重现实现中的第一个构造函数定义：

```
template<class T>
PFArrayBak<T>::PFArrayBak() : PFArray<T>(), usedB(0)
{
    b = new T[getCapacity()];
}
```

请注意，与任何模板类函数的定义一样，它以

```
template<class T>
```

开始。还请注意数组的基类型（new 之后给出）是类型参数 T。其他细节可能不太明显，但是有道理的。

接下来考虑以下行：

```
PFArrayBak<T>::PFArrayBak() : PFArray<T>(), usedB(0)
```

与任何模板类函数的定义一样，定义在作用域解析运算符之前带有 PFArray<T> 和类型参数，但构造函数名只是普通的 PFArrayBak，没有任何类型参数。还请注意基类构造函数在初始化 PFArray<T>() 中包含类型参数 T。这样构造函数就能与接口中以下行的基类型 PFArray<T> 匹配：

```
class PFArrayBak : public PFArray<T>
```

使用模板类 PFArrayBak 的示例程序在图 16.10 中给出。

## Display 16.8 Interface for the Template Class PFArrayBak (part 1 of 2)

```
//This is the header file pfarraybak.h. This is the interface for the
//template class PFArrayBak. Objects of this type are partially filled
//arrays of any type T. This version allows the programmer to make a backup
//copy and restore to the last saved copy of the partially filled array.
#ifndef PFARRAYBAK_H
#define PFARRAYBAK_H
#include "pfarray.h"

namespace PFArraySavitch
{
```

## Display 16.8 Interface for the Template Class PFArrayBak (part 2 of 2)

```
template<class T>
class PFArrayBak : public PFArray<T>
{
public:
    PFArrayBak();
    //Initializes with a capacity of 50.

    PFArrayBak(int capacityValue);

    PFArrayBak(const PFArrayBak<T>& Object);

    void backup();
    //Makes a backup copy of the partially filled array.

    void restore();
    //Restores the partially filled array to the last saved version.
    //If backup has never been invoked, this empties the partially
    //filled array.

    PFArrayBak<T>& operator =(const PFArrayBak<T>& rightSide);

    virtual ~PFArrayBak();
private:
    T *b; //for a backup of main array.
    int usedB; //backup for inherited member variable used.
};
}// PFArraySavitch
#endif //PFARRAY_H
```

## Display 16.9 Implementation for the Template Class PFArrayBak (part 1 of 3)

//This is the file pfarraybak.cpp.
//This is the implementation for the template class PFArrayBak. The
//interface for the template class PFArrayBak is in the file pfarraybak.h.
#include "pfarraybak.h"
#include <iostream>
using std::cout;

namespace PFArraySavitch
{

template<class T>
PFArrayBak<T>::PFArrayBak() : PFArray<T>(), usedB(0)

## Display 16.9 Implementation for the Template Class PFArrayBak (part 2 of 3)

{
    b = new T[getCapacity()];
}

template<class T>
PFArrayBak<T>::PFArrayBak(int capacityValue)
    : PFArray<T>(capacityValue), usedB(0)
{
    b = new T[getCapacity()];
}

template<class T>
PFArrayBak<T>::PFArrayBak(const PFArrayBak<T>& oldObject)
    : PFArray<T>(oldObject), usedB(0)
{
    b = new T[getCapacity()];
    usedB = oldObject.getNumberUsed();
    for (int i = 0; i < usedB; i++)
        b[i] = oldObject.b[i];
}

template<class T>
void PFArrayBak<T>::backup()
{
    usedB = getNumberUsed();
    for (int i = 0; i < usedB; i++)
        b[i] = operator[](i);
}

template<class T>
void PFArrayBak<T>::restore()
{
    emptyArray();

    for (int i = 0; i < usedB; i++)
        addElement(b[i]);
}

template<class T>
PFArrayBak<T>& PFArrayBak<T>::operator =(const PFArrayBak<T>& rightSide)
{
    PFArray<T>::operator =(rightSide);

    if (getCapacity() != rightSide.getCapacity())
    {
        delete [] b;
        b = new T[rightSide.getCapacity()];
    }
}

## Display 16.9 Implementation for the Template Class PFArrayBak (part 3 of 3)

```
    usedB = rightSide.usedB;
    for (int i = 0; i < usedB; i++)
        b[i] = rightSide.b[i];

    return *this;
}
template<class T>
PFArrayBak<T>::~PFArrayBak()
{
    delete [] b;
} // PFArraySavitch
```

## Display 16.10 Demonstration Program for Template Class PFArrayBak (part 1 of 2)

```
//Program to demonstrate the template class PFArrayBak.
#include <iostream>
#include <string>
using std::cin;
using std::cout;
using std::endl;
using std::string;
#include "pfarraybak.h"
#include "pfarraybak.cpp"
#include "pfarraybak.cpp"
using PFArraySavitch::PFArrayBak;
int main()
{
    int cap;
    cout << "Enter capacity of this super array: ";
    cin >> cap;
    PFArrayBak<string> a(cap);
    cout << "Enter " << cap << " strings\n";
    cout << " separated by blanks.\n";
    string next;
    for (int i = 0; i < cap; i++)
    {
        cin >> next;
        a.addElement(next);
    }
```

Do not forget to include the implementation of the base class template

![](img/9505fd46e120aa9c1406715936ff6251_675_0.png)

