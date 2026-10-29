

subversion. 如果派生类的成员函数定义中可以访问基类的私有成员变量，那么成员变量可能会被错误地或以不适当的方式更改。（请记住，访问器和修改器函数可以防止对成员变量进行不适当更改。）

我们将在本章稍后“受保护限定符”小节中讨论一种可能的解决方法，以绕过对基类私有成员变量的此限制。

## 陷阱 私有成员函数实际上并未被继承

如前一陷阱部分所述，基类中为私有的成员变量（或成员函数）在基类的接口和实现之外是无法直接访问的，甚至在派生类的成员函数定义中也无法直接访问。请注意，私有成员函数在不可直接使用方面与私有变量一样。在成员函数的情况下，此限制更为严重。私有变量可以通过访问器或修改器成员函数间接访问。私有成员函数则根本不可用。就好像私有成员函数未被继承一样。

这不应该成为问题。私有成员函数应仅用作帮助函数，因此其使用应限于定义它们的类。如果你希望一个成员函数在多个继承类中用作帮助成员函数，那么它就不仅仅是一个帮助函数，你应该将该成员函数设为 public。

## 受保护限定符

如你所见，你无法在派生类的定义或实现中访问私有成员变量或私有成员函数。存在一种成员变量和函数的分类，允许它们按名称在派生类中被访问，但不能在其他任何地方被访问，例如在非派生类中。如果你在使用成员变量或成员函数前使用限定符 protected 而非 private 或 public，那么对于派生类或函数以外的任何类或函数，其效果就如同该成员变量被标记为 private；然而，在派生类中，该变量可以通过名称访问。

例如，考虑派生自基类 Employee 的类 HourlyEmployee。我们被要求在 HourlyEmployee::printCheck 的定义中使用访问器和修改器成员函数来操作继承的成员变量。如果将类 Employee 中所有私有成员变量改用关键字 protected 而非 private 标记，则派生类 Employee 中 HourlyEmployee::printCheck 的定义可以简化为如下：

```
void HourlyEmployee::printCheck()
//Only works if the member variables of Employee are marked
//protected instead of private.
```
```cpp
{
    netPay = hours * wageRate;

    cout << "\n----------------------------------------------\n";
    cout << "Pay to the order of " << name << endl;
    cout << "The sum of $" << netPay << " Dollars\n";
    cout << "----------------------------------------------\n";
    cout << "Check Stub: NOT NEGOTIABLE\n";
    cout << "Employee Number: " << ssn << endl;
    cout << "Hourly Employee.\nHours worked: " << hours
         << "   Rate: " << wageRate << "   Pay: " << netPay << endl;
    cout << "----------------------------------------------\n";
}
```

在派生类 HourlyEmployee 中，继承的成员变量 name、netPay 和 ssn 可以按名称访问，前提是它们在基类 Employee 中被标记为 protected（而不是 private）。然而，在任何未派生自类 Employee 的类中，这些成员变量都被视为如同被标记为 private。

在基类中标记为 protected 的成员变量在任何派生类中也如同被标记为 protected。例如，假设你定义了类 HourlyEmployee 的派生类 PartTimeHourlyEmployee。类 PartTimeHourlyEmployee 继承了类 HourlyEmployee 的所有成员变量，包括 HourlyEmployee 从类 Employee 继承的成员变量。因此，类 PartTimeHourlyEmployee 将具有成员变量 netPay、name 和 ssn。如果这些成员变量在类 Employee 中被标记为 protected，则它们可以在类 PartTimeHourlyEmployee 的函数定义中使用。

除派生类（以及派生类的派生类等）外，被标记为 protected 的成员变量被视为与被标记为 private 相同。

我们主要包含对 protected 成员变量的讨论，因为你会看到它们被使用并且应该熟悉它们。许多，但并非所有编程权威人士都说使用 protected 成员变量是不良风格，因为这样会损害隐藏类实现的原则。他们说所有成员变量都应标记为 private。如果所有成员变量都标记为 private，则继承的私有成员变量无法按名称在派生类函数定义中访问。然而，这听起来并没有那么糟糕。继承的私有成员变量可以通过调用继承的函数间接访问，这些函数读取或更改私有继承变量。由于权威人士对是否应使用 protected 成员存在分歧，你必须自行决定是否使用它们。

## 受保护成员

如果你在使用成员变量前使用限定符 protected 而非 private 或 public，那么对于派生类或函数以外的任何类或函数，其效果就如同该成员变量被标记为 private。然而，在派生类的成员函数定义中，该变量可以通过名称访问。类似地，如果你在使用成员函数前使用限定符 protected，那么对于派生类或函数以外的任何类或函数，其效果就如同该成员变量被标记为 private。然而，在派生类的成员函数定义中，受保护的函数可以被使用。

受保护成员在派生类中被继承，就如同它们在派生类中被标记为 protected。换句话说，如果一个成员在基类中被标记为 protected，则它可以在所有后代类的定义中按名称访问，而不仅仅是在直接派生自基类的那些类中。

## 自测练习

- 1. 下列程序是否合法（假设已添加适当的 #include 和 using 指令！）？

```
void showEmployeeData(const Employee object);

int main()
{
    HourlyEmployee joe("Mighty Joe",
                        "123-45-6789", 20.50, 40);
    SalariedEmployee boss("Mr. Big Shot",
                          "987-65-4321", 10500.50);
    showEmployeeData(joe);
    showEmployeeData(boss);

    return 0;
}

void showEmployeeData(const Employee object)
{
    cout << "Name: " << object.getName() << endl;
    cout << "Social Security Number: "
         << object.getSsn() << endl;
}
```

- 2. 给出一个类 SmartBut 的定义，它是下面给出的基类 Smart 的派生类。无需考虑 #include 指令或命名空间细节。

```
class Smart
{
```
```
public:
    Smart();
    void printAnswer() const;
protected:
    int a;
    int b;
};

该类应有一个额外的 bool 类型的数据字段 crazy；一个不带参数并返回 bool 类型值的额外成员函数；以及合适的构造函数。新的函数名为 isCrazy。你不需要给出任何实现，只需给出类定义即可。

- 3. 下列是否是派生类 SmartBut 中成员函数 isCrazy 的合法定义，如自测练习 2 中所述？解释你的答案。（请记住，问题问的是是否合法，而不是是否是一个合理的定义。）

```
bool SmartBut::isCrazy() const
{
    if (a > b)
        return crazy;
    else
        return true;
}
```

## ■ 成员函数的重新定义

在派生类 HourlyEmployee 的定义中（Display 14.3），我们给出了新成员函数 setRate、getRate、setHours 和 getHours 的声明。我们还只给出了从类 Employee 继承的成员函数之一的函数声明。未给出函数声明的继承成员函数（如 setName 和 setSsn）保持不变继承。它们在类 HourlyEmployee 中的定义与在基类 Employee 中相同。当你定义像 HourlyEmployee 这样的派生类时，你只列出你想要更改其定义以在派生类中具有不同定义的继承成员函数的函数声明。如果你查看类 HourlyEmployee 的实现（Display 14.5），你会看到我们重新定义了继承的成员函数 printCheck。类 SalariedEmployee 也对成员函数 printCheck 提供了新的定义，如 Display 14.6 所示。而且，这两个类给出了不同的定义。函数 printCheck 在派生类中被重新定义。

Display 14.7 给出了一个演示程序，说明了派生类 HourlyEmployee 和 SalariedEmployee 的使用。

