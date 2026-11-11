
```cpp
Derived()
{
    cout<<"Derived class constructor calling"<<endl;
}
~Derived()
{
    cout<<"Derived class destructor calling"<<endl;
}
void MyFuncD()
{
    cout<<"Function of derived class"<<endl;
}
};

int main()
{
    Derived d(38);
    cout<<"Main Program started"<<endl;
    d.MyFuncD();
    cout<<"Main Program ended"<<endl;
    return 0;
}
```

在清单 9 中，编译器会生成以下错误：

> 错误：找不到与‘Derived::Derived(int)’匹配的项

有两种解决方案可以避免上述错误。可描述如下：

-   派生类必须有自己的构造函数，其签名与基类构造函数相似
-   派生类具有带参构造函数，并显式地将参数传递给基类构造函数

清单 10 表明，在派生类中包含带参构造函数可以解决调用基类重载构造函数的问题（你可以在 CD 的 Code\Chapter7 文件夹中找到 DerivedParameterizedConstructor.cpp 文件）：

### ▶ 清单 10：在派生类中添加带参构造函数

```cpp
#include<iostream.h>

class Base
{
  public:
    Base()
    {
      cout<<"Base class constructor (no parameter) calling"<<endl;
    }
    Base(int x)
    {
        cout<<"Base class constructor with one parameter calling"<<endl;
        cout<<"Parameter value is : "<<x<<endl;
    }
    ~Base()
    {
        cout<<"Base class destructor calling"<<endl;
    }
    void MyFuncB()
    {
        cout<<"Function of derived class"<<endl;
    }
};
class Derived:public Base
{

public:

Derived()
{
    cout<<"Derived class constructor calling"<<endl;
}
Derived(int x)
{
    cout<<"Derived class constructor with one parameter calling"<<endl;
    cout<<"Parameter value is : "<<x<<endl;
}
~Derived()
{
    cout<<"Derived class destructor calling"<<endl;
}
void MyFuncD()
{
    cout<<"Function of derived class"<<endl;
}
};

int main()
{
    Derived d(38);
    cout<<"Main Program started"<<endl;
    d.MyFuncD();
    cout<<"Main Program ended"<<endl;
    return 0;

}
```

### 输出

```text
Base class constructor (no parameter) calling
Derived class constructor with one parameter calling
Parameter value is : 38
Main Program started
Function of derived class
Main Program ended
Derived class destructor calling
Base class destructor calling
```

在清单 10 中，创建了 Base 类和 Derived 类，其中 Derived 类继承自 Base 类。Base 类的成员包括一个默认构造函数、一个带参构造函数、一个析构函数以及 MyFuncB() 函数，而 Derived 类的成员包括一个默认构造函数、一个带参构造函数、一个析构函数以及 MyFuncD() 函数。

在 main() 函数中，创建了 Derived 类的对象 d，该对象会调用 Base 类的默认构造函数、Derived 类的带参构造函数以及这两个类的析构函数。此外，d 对象在 Main Program started 和 Main Program ended 语句之间调用其自身类的 MyFuncD() 函数。

然而，可能存在需要调用基类的带参构造函数的情况。在这种情况下，派生类的对象会调用派生类构造函数，该构造函数接受一个参数。此构造函数通过将参数值传递给基类构造函数的形参来调用基类构造函数。这可以通过声明派生类构造函数来实现，如下面的代码片段所示：

```cpp
Derived(int x):Base(x)
{

    //body of the constructor
}
```

清单 11 展示了派生类的带参构造函数如何显式调用基类构造函数（你可以在 CD 的 Code\Chapter7 文件夹中找到 ExplicitInvokeBaseConstructor.cpp 文件）：

### ▶ 清单 11：显式调用基类构造函数

```cpp
#include<iostream.h>

class Base
{
    public:
        Base(int x)
        {
            cout<<"Base class constructor with one parameter calling"<<endl;
            cout<<"Parameter value is : "<<x<<endl;
        }
        ~Base()
        {
            cout<<"Base class destructor calling"<<endl;
        }
        void MyFuncB()
        {
            cout<<"Function of derived class"<<endl;
        }
};

class Derived:public Base
{
public:
    Derived(int x):Base(x)
    {
        cout<<"Derived class constructor with one parameter calling"<<endl;
        cout<<"Parameter value is : "<<x<<endl;
    }
    ~Derived()
    {
        cout<<"Derived class destructor calling"<<endl;
    }
    void MyFuncD()
    {
        cout<<"Function of derived class"<<endl;
    }
};

int main()
{
    Derived d(38);
    cout<<"Main Program started"<<endl;
    d.MyFuncD();
    cout<<"Main Program ended"<<endl;
    return 0;
}
```

### 输出

```text
Base class constructor with one parameter calling
Parameter value is : 38
Derived class constructor with one parameter calling
Parameter value is : 38
Main Program started
Function of derived class
Main Program ended
Derived class destructor calling
Base class destructor calling
```

在清单 11 中，创建了 Base 类和 Derived 类，其中 Derived 类继承自 Base 类。Base 类的成员包括一个默认构造函数、一个带参构造函数、一个析构函数以及 MyFuncB() 函数。Derived 类的成员包括一个默认构造函数、一个带参构造函数、一个析构函数以及 MyFuncD() 函数。Derived 类的带参构造函数会显式地将参数传递给 Base 类的带参构造函数。

在 main() 函数中，创建了 Derived 类的对象 d，该对象会调用 Base 类和 Derived 类的带参构造函数与析构函数。此外，d 对象在 Main Program started 和 Main Program ended 语句之间调用其自身类的 MyFuncD() 函数。

由此可以得出结论：只要基类具有默认（无参）构造函数，派生类就不需要构造函数。然而，如果基类构造函数带有参数，则派生类也必须具有带参构造函数。此外，派生类构造函数会显式地将值传递给基类构造函数的实参。创建派生类的对象时，先执行基类的构造函数，再执行派生类的构造函数。然而，对于析构函数，这一顺序是相反的，即先执行派生类的析构函数，再执行基类的析构函数。

在学习了如何调用基类和派生类的构造函数与析构函数之后，我们来讨论如何创建容器类。

## 7.7 创建容器类

容器类是其他类的对象容器。它表示将某个类的属性继承到另一个类中的一种间接方式。这意味着容器类的对象是若干其他对象的集合。创建容器类的目的是保存另一个类的多个实例。创建容器类的语法是：

```cpp
class Class_Name
{
};
class ContainerClass_Name
{
Class_Name object_name;
};
```

在上述语法中，ContainerClass_Name 表示容器类的名称，该容器类包含 Class_Name 类的 object_name 对象的声明。

清单 12 展示了容器类的一个示例（你可以在 CD 的 Code\Chapter7 文件夹中找到 ContainerClass.cpp 文件）：

### ▶ 清单 12：创建容器类

```cpp
#include<iostream.h>
#include<string.h>

class Alphabets
{
char day_element;
public:
void setAlphabet(char);
void showAlphabet();
};

class Day
{
Alphabets objchar[10];
int l;

public:

void setDay(char*);
int getDayLength();
void showDay();
};

class week
{
Day objDay[7];
int l;
public:

void setweek(char**);
void showweek();
};

void Alphabets::setAlphabet(char c)
{
day_element=c;
}
void Alphabets::showAlphabet()
{
cout<<day_element;
}

void Day::setDay(char* c)
{
```
