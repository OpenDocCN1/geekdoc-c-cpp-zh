

## 4. (Modify) a. 修改程序 12.1 以包含一个名为 Sphere 的派生类，该派生类继承自基类 Circle。Sphere 的唯一额外类成员应为构造函数和一个返回球体体积的 calcval() 函数。 （注意：体积 = 4 / 3 πr³。） b. 将练习 4a 中构建的类包含在一个可工作的 C++ 程序中。让你的程序调用 Sphere 类中的所有成员函数。

## 5. (Program) a. 创建一个名为 Point 的基类，包含表示点坐标的 x 和 y 数据成员。从该类派生一个名为 Circle 的类，再包含一个名为 radius 的数据成员。对于该派生类，x 和 y 数据成员表示圆的圆心坐标。Point 类的成员函数应包括构造函数、返回 0 的 area() 函数，以及返回两点 (x₁, y₁) 和 (x₂, y₂) 之间距离的 distance() 函数，其中 distance = √((x₂ - x₁)² + (y₂ - y₁)²) 此外，派生类应具有构造函数和一个重写函数 named area()，该函数返回圆的面积。 b. 将练习 5a 中构建的类包含在一个可工作的 C++ 程序中。让你的程序调用每个类中的所有成员函数。此外，使用两个 Circle 对象调用基类的 distance() 函数并解释该函数返回的结果。

## 6. (Modify) a. 使用练习 5a 中构建的类，从 Circle 类派生一个名为 Cylinder 的类。Cylinder 类应具有构造函数和一个名为 area() 的成员函数，用于确定圆柱体的表面积。对于该函数，使用算法 surface area = 2πr(l + r)，其中 r 为圆柱体的半径，l 为长度。 b. 将练习 6a 中构建的类包含在一个可工作的 C++ 程序中。让你的程序调用 Cylinder 类中的所有成员函数。 c. 你认为如果使用两个 Cylinder 对象调用 Point（基）类的 distance() 函数，结果会怎样？

## 7. (Program) a. 创建一个名为 Rectangle 的基类，包含 length 和 width 数据成员。从该类派生一个名为 Box 的类，再包含一个名为 depth 的数据成员。基类 Rectangle 的成员函数应包括构造函数和 area() 函数。派生类 Box 应具有构造函数、volume() 函数，以及一个重写函数 named area()，该函数返回盒子的表面积。 b. 将练习 7a 中构建的类包含在一个可工作的 C++ 程序中。让你的程序调用每个类中的所有成员函数，并手动验证结果。

## 12.2 多态性

如前所述，多态性允许使用相同的函数名在基类的对象中调用一种响应，在派生类的对象中调用另一种响应。通过使用重载的派生成员函数覆盖基成员函数，如程序 12.1 中 calcval() 函数所示，是多态性的一个例子。然而，在某些情况下，这种覆盖方法的工作方式可能与你期望的不同。要理解原因，请看程序 12.2。

### Program 12.2

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
```cpp
int main()
{
    One object_1;  // object_1 is an object of the base class
    Two object_2;  // object_2 is an object of the derived class

    // call f2() using a base class object call
    cout << "The computed value using a base class object call is "
         << object_1.f2() << endl;

    // call f2() using a derived class object call
    cout << "The computed value using a derived class object call is "
         << object_2.f2() << endl;

    return 0;
}
```
```

程序 12.2 产生的输出如下：

```
The computed value using a base class object call is 36
The computed value using a derived class object call is 36
```

正如该输出所示，无论哪种对象类型调用 `f2()` 函数，结果都相同，因为派生类没有覆盖基类的 `f2()` 函数。因此，对 `f2()` 的两次调用都会导致调用基类的 `f2()` 函数。

在基类的 `f2()` 函数被调用后，它总是调用基类的 `f1()` 版本，而不是派生类重写过的版本。这种行为是由一种称为 **函数绑定** 的过程引起的。在正常的函数调用中，使用 **静态绑定**，意味着确定调用哪个函数的决定是在编译时做出的。因此，当编译器第一次遇到基类中的 `f1()` 函数时，它就确定了无论 `f2()` 是从基类还是派生类对象调用，它随后都会调用基类的 `f1()` 函数。

如果不使用静态绑定，假设你想使用一种能够在运行时根据调用对象的类型确定应调用哪个函数的绑定方法。这种类型的绑定称为 **动态绑定**，在 C++ 中通过虚函数实现。**虚函数** 告诉编译器创建一个指向函数的指针，但在函数实际被调用之前不填充指针的值。然后在运行时，*基于发出调用的对象*，使用适当的函数地址。

创建虚函数很容易——只需在类声明部分在函数的返回类型前加上关键字 `virtual` 即可。例如，查看程序 12.3，它与程序 12.2 相同，只是 `f1()` 函数被声明为虚函数。

### Program 12.3

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
        One(double = 2.0);      // constructor
        virtual double f1(double);  // a member function
        double f2(double);          // another member function
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
        virtual double f1(double);   // overrides class One's f1()
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

```
The computed value using a base class object call is 36
The computed value using a derived class object call is 16
```

正如该输出所示，f2() 函数现在根据发出调用的对象类型调用重载的 f1() 函数的不同版本。基于发出调用的对象进行选择是多态行为的经典定义，并且是由对 f1() 施加的动态绑定引起的，因为它是虚函数。

在函数被声明为虚函数后，它对下一个派生类保持虚函数，无论派生类中是否有虚声明。因此，派生类中的第二个虚声明在严格意义上不是必需的，但应包含以提高清晰度，并确保任何随后派生的类正确继承该函数。

在图 12.5 的继承图中，类 C 派生自类 B，类 B 派生自类 A。1 在这种情况下，如果 f1() 函数在类 A 中是虚函数但未在类 B 中声明，则它在类 C 中不是虚函数。唯一的其他要求是，在函数被声明为虚函数后，所有后续派生类重写版本的返回类型和参数列表必须相同。

![](img/e9bf940282dfb289356f077151cc69dd_570_0.png)

# Figure 12.5 An inheritance diagram

> 1按惯例，如第 12.1 节所述，箭头始终从派生类指向基类。

