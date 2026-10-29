

# 程序 12.2

```
#include <iostream>
#include <cmath>
using namespace std;

// class declaration section for the base class
class One
{
    protected:
        double a;
    public:
        One(double = 2.0);  // constructor
        double f1(double);  // a member function
        double f2(double);  // another member function
};

// class implementation section for One
One::One(double val)  // constructor
{
    a = val;
}

double One::f1(double num)  // a member function
{
    return(num/2);
}

double One::f2(double num)  // another member function
{
    return( pow(f1(num),2) );  // square the result of f1()
}

// class declaration section for the derived class
class Two : public One
{
    public:
        double f1(double);  // this overrides class One's f1()
};

// class implementation section for Two
double Two::f1(double num)
{
    return(num/3);
}
```

```
int main()
{
    One object_1;  // object_1 is an object of the base class
    Two object_2;  // object_2 is an object of the derived class

    // call f2() using a base class object call
    cout << "The computed value using a base class object call is "
         << object_1.f2(12) << endl;

    // call f2() using a derived class object call
    cout << "The computed value using a derived class object call is "
         << object_2.f2(12) << endl;

    return 0;
}
```

程序 12.2 产生的输出如下：

The computed value using a base class object call is 36
The computed value using a derived class object call is 36

正如该输出所示，无论哪种对象类型调用 f2() 函数，结果都相同，因为派生类没有重写基类的 f2() 函数。因此，对 f2() 的两次调用都导致调用基类的 f2() 函数。

在基类的 f2() 函数被调用后，它始终调用基类版本的 f1()，而不是派生类的重写版本。这种行为是由一个称为函数绑定 的过程引起的。在正常的函数调用中，使用静态绑定，这意味着确定调用哪个函数是在编译时完成的。因此，当编译器首次遇到基类中的 f1() 函数时，它就确定无论 f2() 是由基类对象还是派生类对象调用，其后都会调用基类的 f1() 函数。

如果不使用静态绑定，假设你希望使用一种能够在运行时根据发出调用的对象类型确定应调用哪个函数的绑定方法。这种类型的绑定称为动态绑定，在 C++ 中通过虚函数实现。虚函数告诉编译器创建一个指向函数的指针，但不要在函数实际被调用之前填充指针的值。然后在运行时，基于发出调用的对象，使用适当的函数地址。

创建虚函数很容易——只需在类声明部分在函数的返回类型前加上关键字 virtual 即可。例如，查看程序 12.3，它与程序 12.2 相同，只是 f1() 函数声明为虚函数。

# 程序 12.3

```
#include <iostream>
#include <cmath>
using namespace std;

// class declaration section for the base class
class One
{
    protected:
        double a;
    public:
        One(double = 2.0);          // constructor
        virtual double f1(double);  // a member function
        double f2(double);           // another member function
};

// class implementation section for One
One::One(double val)   // constructor
{
    a = val;
}

double One::f1(double num)   // a member function
{
    return(num/2);
}

double One::f2(double num)   // another member function
{
    return( pow(f1(num),2) );  // square the result of f1()
}

// class declaration section for the derived class
class Two : public One
{
    public:
        virtual double f1(double);    // overrides class One's f1()
};

// class implementation section for Two
double Two::f1(double num)
{
    return(num/3);
}
```

```
int main()
{
    One object_1;  // object_1 is an object of the base class
    Two object_2;  // object_2 is an object of the derived class

    // call f2() using a base class object call
    cout << "The computed value using a base class object call is "
         << object_1.f2(12) << endl;

    // call f2() using a derived class object call
    cout << "The computed value using a derived class object call is "
         << object_2.f2(12) << endl;

    return 0;
}
```

程序 12.3 产生以下输出：

The computed value using a base class object call is 36

The computed value using a derived class object call is 16

正如该输出所示，f2() 函数现在根据发出调用的对象类型调用重载的 f1() 函数的不同版本。基于发出调用的对象进行选择是多态行为的经典定义，并且是由对 f1() 施加的动态绑定引起的，因为它是虚函数。

在函数被声明为虚函数后，它对下一个派生类保持虚函数，无论派生类中是否有虚函数声明。因此，派生类中的第二个虚函数声明严格来说不是必要的，但应包含在内以提高清晰度，并确保任何随后派生的类正确继承该函数。

在图 12.5 的继承图中，类 C 由类 B 派生，类 B 由类 A 派生。¹ 在这种情况下，如果 f1() 函数在类 A 中是虚函数，但在类 B 中未声明，则它在类 C 中不是虚函数。唯一的其他要求是，在函数被声明为虚函数后，所有后续派生类重写版本的返回类型和参数列表必须相同。

![](img/202cface8244f523c2641baa2e00d7dd_570_0.png)

# 图 12.5 一个继承图

![](img/202cface8244f523c2641baa2e00d7dd_571_0.png)

# 练习 12.2

- 1. **(练习)** 输入并运行程序 12.2 和 12.3，以便你理解每个程序中函数调用之间的关系。
- 2. **(复习)** 描述静态绑定和动态绑定之间的区别。
- 3. **(复习)** 描述虚函数和非虚函数之间的区别。
- 4. **(复习)** 解释什么是多态性，并给出多态行为的例子。
- 5. **(复习)** 描述 C++ 提供的实现多态性的两种方法。
- 6. **(复习)** 解释为整数和双精度内置类型提供的乘法运算符是重载的例子还是多态性的例子。

# 12.3 动态对象创建和删除

当程序中定义每个对象时，编译器为其指定足够的存储空间；在程序运行之前，该存储空间随后从计算机内存位置的池中分配。内存位置分配后，它们在对象的生命周期内保持固定，或直到程序运行结束。例如，如果 `main()` 函数声明了三个 Date 对象，则这些对象的存储空间从定义点起保持固定，直到 `main()` 执行完成。

这种固定分配内存存储位置的替代方案是 **动态分配** 内存，其中要分配的存储量是在运行时根据请求分配，而不是在编译时固定。动态分配内存在使用列表和对象时很有用，因为它允许在添加新项目时扩展列表，并在删除项目时收缩列表。对于面向对象的程序，它允许根据需要创建和销毁新对象。

作为动态对象创建的示例，假设你正在创建一个程序，旨在跟踪大型连锁店自助结账机中客户的流动。你事先不知道每个收银台发生的交易数量。然而，通过使用动态分配，程序可以在每次结账交易发生时创建一个对象，以跟踪客户对结账过程的使用。该对象可能包括结账的商品数量和每个客户到达收银台的时间。虽然该类的无操作方法稍后完成，但以下类足以定义该对象所需的信息。在查看此类时，请注意阴影的构造函数和析构函数方法：

// class declaration section
class Checkout
{
  private:
    int numItems;
    double arrivalTime;

![](img/202cface8244f523c2641baa2e00d7dd_571_1.png)

