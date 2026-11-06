
编译器将允许从指向派生类对象的基类指针访问仅派生类成员，**如果**我们将基类指针显式转换为派生类指针——这称为**向下转型**。如你所知，可以让基类指针指向派生类对象。然而，正如我们在**图 12.3**中演示的，基类指针*只能*用于调用基类中声明的函数。向下转型允许通过基类指针所指向的派生类对象执行派生类特有的操作。向下转型是一种潜在*危险*的操作。**12.9 节**演示如何*安全地*使用向下转型。

## 12.4 虚函数与虚析构函数

在**12.3.1 节**中，我们让一个基类 `CommissionEmployee` 指针指向派生类 `BasePlusCommissionEmployee` 对象，然后通过该指针调用成员函数 `toString`。回想一下，*句柄的类型*决定了调用哪个类的功能。在那种情况下，`CommissionEmployee` 指针在 `BasePlusCommissionEmployee` 对象上调用了 `CommissionEmployee` 成员函数 `toString`，即使该指针指向的是一个拥有自己自定义 `toString` 函数的 `BasePlusCommissionEmployee` 对象。

### 12.4.1 为什么 `virtual` 函数有用

假设 `Circle`、`Triangle`、`Rectangle` 和 `Square` 等形状类都派生自基类 `Shape`。这些类中的每一个都可能通过成员函数 `draw` 获得*绘制自身*的能力，但每个形状的函数大不相同。在绘制一组形状的程序中，能够将所有形状*一般地*视为基类 `Shape` 的对象会很有用。然后，要绘制任何形状，我们只需使用基类 `Shape` 指针调用函数 `draw`，并让程序根据基类 `Shape` 指针在任意给定时刻所指向的对象类型，*动态地*（即运行时）确定使用哪个派生类的 `draw` 函数。这就是*多态行为*。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1563_0.png)

### 软件工程观察 12.3

*使用* `virtual` *函数时，对象的类型——而不是用于调用该对象成员函数的句柄类型——决定调用哪个版本的* `virtual` *函数。*

### 12.4.2 声明 `virtual` 函数

为了实现这种行为，我们在基类中将 `draw` 声明为**虚函数**，并在*每个*派生类中**重写** `draw` 以绘制相应的形状。从实现的角度来看，*重写*函数与*重新定义*函数没有区别（后者是我们到目前为止一直采用的方法）。派生类中被重写的函数具有与其基类中被重写函数*相同的签名和返回类型*（即*原型*）。如果我们*不*将基类函数声明为 `virtual`，就可以*重新定义*该函数。

相比之下，如果我们*确实*将基类函数声明为 `virtual`，就可以*重写*该函数以启用*多态行为*。在基类中，在函数原型前加上关键字 `virtual` 即可声明 `virtual` 函数。例如，

```cpp
virtual void draw() const;
```

将出现在基类 `Shape` 中。前一个原型声明函数 `draw` 是一个 `virtual` 函数，不接受参数且不返回值。该函数被声明为 `const`，因为 `draw` 函数通常不会修改调用它的 `Shape` 对象。虚函数*不必*是 `const` 函数。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1565_0.png)

### 软件工程观察 12.4

*一旦函数被声明为 `virtual`，从那时起，它沿着继承层次向下始终保持为 `virtual`，即使派生类在重写它时没有显式声明为 `virtual`。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1565_1.png)

### 良好编程实践 12.1

*尽管由于类层次结构中较高层的声明，某些函数隐式地成为 `virtual`，但为了清晰起见，应在类层次结构的每一层显式地将这些函数声明为 `virtual`。*

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1565_2.png)

### 软件工程观察 12.5

*当派生类选择不重写其基类的 `virtual` 函数时，派生类只是继承其基类的 `virtual` 函数实现。*

### 12.4.3 通过基类指针或引用调用 `virtual` 函数

如果程序通过指向派生类对象的基类指针（例如 `shapePtr->draw()`）或通过派生类对象的基类引用（例如 `shapeRef.draw()`）调用 `virtual` 函数，程序将*根据对象类型——而不是指针或引用类型——动态地*（即执行时）选择正确的派生类函数。在选择执行时（而不是编译时）调用哪个合适的函数称为**动态绑定**。

### 12.4.4 通过对象名称调用 `virtual` 函数

当通过*名称*引用特定对象并使用点成员选择运算符（例如 `squareObject.draw()`）来调用 `virtual` 函数时，函数调用在*编译时解析*（这称为**静态绑定**），并且所调用的 `virtual` 函数是为该特定对象的类定义（或继承）的函数——这*不是*多态行为。`virtual` 函数的动态绑定仅通过指针和引用发生。

### 12.4.5 `CommissionEmployee` 层次结构中的 `virtual` 函数

现在让我们看看 `virtual` 函数如何在我们的员工层次结构中启用多态行为。**图 12.4–12.5** 分别是类 `CommissionEmployee` 和 `BasePlusCommissionEmployee` 的头文件。我们修改了这些头文件，将每个类的 `earnings` 和 `toString` 成员函数声明为 `virtual`（**图 12.4** 的第 28–29 行和**图 12.5** 的第 17–18 行）。因为函数 `earnings` 和 `toString` 在类 `CommissionEmployee` 中是 `virtual`，所以类 `BasePlusCommissionEmployee` 的 `earnings` 和 `toString` 函数**重写**类 `CommissionEmployee` 的对应函数。此外，类 `BasePlusCommissionEmployee` 的 `earnings` 和 `toString` 函数使用 C++11 的 **override** 关键字声明。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1569_0.png)

### 错误预防提示 12.1

*为帮助防止错误，请将 C++11 的 `override` 关键字应用于每个重写基类 `virtual` 函数的派生类函数原型。这使编译器能够检查基类是否具有签名相同的 `virtual` 成员函数。如果没有，编译器会生成错误。这不仅确保你使用适当的签名重写基类函数，还能防止你不小心隐藏具有相同名称但不同签名的基类函数。*

现在，如果我们将基类 `CommissionEmployee` 指针指向派生类 `BasePlusCommissionEmployee` 对象，并且程序使用该指针调用函数 `earnings` 或 `toString`，则将*多态地*调用 `BasePlusCommissionEmployee` 对象的对应函数。类 `CommissionEmployee` 和 `BasePlusCommissionEmployee` 的成员函数实现没有更改，因此我们复用**图 11.14** 和 **11.15** 中的版本。

```cpp
// Fig. 12.4: CommissionEmployee.h
// CommissionEmployee class with virtual earnings and toString functions.
#ifndef COMMISSION_H
#define COMMISSION_H

#include <string> // C++ standard string class

class CommissionEmployee {
public:
    CommissionEmployee(const std::string& first, const std::string&,
        const std::string& ssn, double = 0.0, double = 0.0);

    void setFirstName(const std::string&); // set first name
    std::string getFirstName() const; // return first name

    void setLastName(const std::string&); // set last name
    std::string getLastName() const; // return last name

    void setSocialSecurityNumber(const std::string&); // set SSN
    std::string getSocialSecurityNumber() const; // return SSN

    void setGrossSales(double); // set gross sales amount
    double getGrossSales() const; // return gross sales amount

    void setCommissionRate(double); // set commission rate (percentage)
    double getCommissionRate() const; // return commission rate

    virtual double earnings() const; // calculate earnings
    virtual std::string toString() const; // string representation
private:
    std::string firstName;
    std::string lastName;
    std::string socialSecurityNumber;
    double grossSales; // gross weekly sales
    double commissionRate; // commission percentage
};

#endif
```

**图 12.4** `CommissionEmployee` 类头文件将 `earnings` 和 `toString` 声明为 `virtual`。

