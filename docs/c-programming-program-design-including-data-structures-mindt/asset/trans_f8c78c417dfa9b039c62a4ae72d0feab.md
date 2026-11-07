
首先，让我们讨论形参是引用参数或指针的情况。具体来说，考虑以下类：

```cpp
class petType
{
public:
    void print() const;
    petType(string n = "");

private:
    string name;
};

class dogType: public petType
{
public:
    void print() const;
    dogType(string n = "", string b = "");

private:
    string breed;
};
```

类 `petType` 有三个成员。类 `dogType` 派生自类 `petType`，并且有自己的三个成员。两个类都有一个成员函数 `print`。假设这两个类的成员函数定义如下：

```cpp
void petType::print() const
{
    cout << "Name: " << name;
}

petType::petType(string n)
{
    name = n;
}

void dogType::print() const
{
    petType::print();
    cout << ", Breed: " << breed << endl;
}

dogType::dogType(string n, string b)
    : petType(n)
{
    breed = b;
}
```

考虑用户程序（客户端代码）中的以下函数：

```cpp
void callPrint(petType& p)
{
    p.print();
}
```

函数 `callPrint` 有一个 `petType` 类型的形参引用 p。你可以使用 `petType` 类型或 `dogType` 类型的对象作为参数来调用函数 `callPrint`。此外，函数 `callPrint` 的函数体调用成员函数 `print`。考虑以下函数 main：

```cpp
int main()                                      //Line 1
{
    petType pet("Lucky");                       //Line 2
    dogType dog("Tommy", "German Shepherd");    //Line 4

    pet.print();                                  //Line 5
    cout << endl;                                 //Line 6
    dog.print();                                  //Line 7

    cout << " *** Calling the function callPrint ***" //Line 8
         << endl;
    callPrint(pet);                               //Line 9
    cout << endl;                                 //Line 10
    callPrint(dog);                               //Line 11
    cout << endl;                                 //Line 12

    return 0;                                     //Line 13
}                                                //Line 14
```

## 示例运行

```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy
```

第 3 行到第 8 行的语句非常直接。让我们看看第 9 行和第 11 行的语句。第 9 行的语句调用函数 `callPrint`，并将对象 pet 作为参数传递；它生成输出的第四行。第 11 行的语句也调用函数 `callPrint`，但将对象 dog 作为参数传递；它生成输出的第五行。第 9 行和第 11 行的语句生成的输出只显示 name 的值，尽管每次传递的是不同类的对象作为参数。因为在第 11 行，对象 dog 被作为参数传递给函数 `callPrint`，人们会期望第 11 行语句生成的输出应该与输出的第二行相同。实际发生的是，对于这两个语句（第 9 行和第 11 行），执行的是基类 `petType` 的成员函数 `print`。这是因为函数 `callPrint` 函数体中成员函数 `print` 的绑定发生在编译时。由于函数 `callPrint` 的形参 p 是 `petType` 类型，编译器为语句 `p.print();` 关联类 `petType` 的函数 `print`。更具体地说，在编译时绑定中，调用特定函数所需的代码由编译器生成。（编译时绑定也称为静态绑定或早期绑定。）

对于第 11 行的语句，实际参数的类型是 **dogType**。因此，当函数 **callPrint** 的函数体执行时，逻辑上应该执行对象 dog 的 **print** 函数，但事实并非如此。那么，在程序执行期间，C++ 如何纠正这个调用适当函数的问题呢？C++ 通过提供 **虚函数** 机制来纠正这个问题。虚函数的绑定发生在程序执行时，而不是编译时。这种绑定称为 **运行时绑定、后期绑定或动态绑定**。更正式地说，在运行时绑定中，编译器不生成调用特定函数的代码。相反，它生成足够的信息，使运行时系统能够为适当的函数调用生成特定代码。运行时绑定也称为 **动态绑定**。

在 C++ 中，虚函数使用保留字 `virtual` 声明。让我们使用这个特性重新定义前面的类。

```cpp
class petType
{
public:
    virtual void print() const;        //virtual function
    petType(string n = "");

private:
    string name;
};

class dogType: public petType
{
public:
    void print() const;
    dogType(string n = "", string b = "");

private:
    string breed;
};
```

注意，我们只需要在基类中声明虚函数。

dogType 成员函数 print 的定义与之前相同。因为我们在基类中放置了虚函数声明，基类对象可以使用派生类的定义。例如，如果我们执行经过这些修改的前一个程序，输出如下：

## 示例运行

```text
Name:  Lucky
Name:  Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name:  Lucky
Name:  Tommy, Breed: German Shepherd
```

这个输出表明，对于第 11 行的语句，执行的是 dogType 的 print 函数（见输出的最后两行）。

前面的讨论也适用于形参是指向类的指针，并且派生类的指针作为实际参数传递的情况。为了说明这个特性，假设我们有前面的类。（我们假设类 `petType` 的定义在头文件 `petType.h` 中，类 `dogType` 的定义在头文件 `dogType.h` 中。）考虑以下程序：

```cpp
#include <iostream>
#include "petType.h"
#include "dogType.h"

using namespace std;

void callPrint(petType *p);

int main()
{
        petType *q;                                      //Line 1
        dogType *r;                                       //Line 2
                                                        //Line 3
                                                        //Line 4
        q = new petType("Lucky");                        //Line 5
        r = new dogType("Tommy", "German Shepherd");    //Line 6

        q->print();                                      //Line 7
        cout << endl;                                    //Line 8
        r->print();                                      //Line 9

        cout << "*** Calling the function callPrint  ***"
             << endl;                                    //Line 10
        callPrint(q);                                    //Line 11
        cout << endl;                                     //Line 12
        callPrint(r);                                    //Line 13

        return 0;                                        //Line 14
}                                                       //Line 15

void callPrint(petType *p)
{
        p->print();
}
```

## 示例运行

```text
Name: Lucky
Name: Tommy, Breed: German Shepherd
*** Calling the function callPrint ***
Name: Lucky
Name: Tommy, Breed: German Shepherd
```

前面的示例表明，如果形参（比如类类型的 p）是引用参数或指针，并且 p 使用基类的虚函数，我们可以有效地将派生类对象作为实际参数传递给 p。

然而，如果 p 是值参数，那么这种将派生类对象作为实际参数传递给 p 的机制就不起作用，即使 p 使用虚函数。
