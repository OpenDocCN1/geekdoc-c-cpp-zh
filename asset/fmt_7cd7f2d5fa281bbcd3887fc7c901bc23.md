
正如注释所示，这是行不通的。成员变量 `netPay` 是 `Employee` 类中的一个 `private` 成员变量，尽管像 `HourlyEmployee` 这样的派生类继承了它，但并不能直接访问它。你必须使用某些成员函数来访问私有变量 `netPay`。在 `HourlyEmployee` 类中完成 `printCheck` 定义的正确方法是显示 14.5 中的做法（之前已显示了部分）。

`name` 和 `netPay` 是继承变量这一事实也解释了为什么我们在 `HourlyEmployee::printCheck` 的定义中需要使用访问函数 `getName` 和 `getPay`，而不是直接使用变量 `name` 和 `netPay`。你不能通过名称直接提到一个私有的继承变量。你必须使用在基类中定义的公共访问函数和修改器函数（如 `get` 和 `setName`）。（记住，访问函数是允许你访问类成员变量的函数，而修改器函数是允许你更改类成员变量的函数。访问函数和修改器函数将在第6 章介绍。）

基类的私有变量无法在派生类的成员函数定义中被访问，这一事实对某些人来说似乎是错误的。毕竟，如果你是一个员工并想更改名字，没人会说：“对不起，我是 `Employee` 类的一个私有成员。”如果你是一个员工，你同样是一个员工。在 Java 中也是如此的；`HourlyEmployee` 类的对象也是 `Employee` 类的对象。但在 C++ 中，允许访问私有成员变量，然后如果你想访问一个私有变量，你只需创建一个派生类并在该类的成员函数中访问它。

## 第14 章 继承

### 陷阱：（续）

这意味着所有私有成员变量对于任何愿意多花一点精力的人都是可访问的。这种场景说明了问题，但更大的问题是无意中的错误，而非故意的破坏。如果类的私有成员变量在派生类的成员函数定义中是可以访问的，那么成员变量可能会被错误地或以不当的方式更改。（记住，访问函数和修改器函数可以防止成员变量发生不当更改。）

我们将在本章稍后的“`protected` 修饰符”小节中，讨论绕过这一基类私有成员变量限制的一种可能方法。

## 陷阱：私有成员函数实际上没有被继承

正如上一个陷阱节所述，基类中为 `private` 的成员变量（或成员函数）在派生类的成员函数定义中是不可访问的。注意，私有函数与私有变量一样，在可用方面是不可用的。对于成员函数，情况更为严重。私有变量可以通过访问或修改函数间接访问，而私有函数直接是不可用的。这就像私有函数没有被继承一样。

这不应该是一个问题。私有函数应该仅作为辅助函数，且其使用应限制在定义它们的类中。如果你希望一个私有函数在多个类中作为辅助函数使用，那么你应该将其设为 `public`。

## `protected` 修饰符

正如你所看到的，在派生类的成员函数定义中无法访问私有成员变量或私有函数。如果你对成员变量或函数使用 `protected` 修饰符而不是 `private`，对于派生类以外的任何类，效果与标记为 `private` 相同。

## 继承基础

例如，考虑派自基类 `Employee` 的 `HourlyEmployee` 类。我们在 `HourlyEmployee::printCheck` 的定义中使用访问和修改函数来操作继承的成员变量。如果 `Employee` 的所有成员变量标记为 `protected` 而不是 `private`，那么派生类中的 `printCheck` 定义可以简化为：

```
void HourlyEmployee::printCheck() {

    // 如果 Employee 的成员变量是
    // protected 而不是 private。
    netPay = hours * wageRate;

    cout << "Pay to the order of " << name << endl;
    cout << "The sum of " << netPay << " Dollars\n";
    cout << "Check Stub: Not NEGOTABLE\n";
    cout << "HourlyEmployee: " << ssn << endl;
    cout << "HourlyEmployee.hours worked: " << hours << endl;
    cout << "Rate: " << wageRate << " Pay: " << netPay << endl;
}
```

在派生类 `HourlyEmployee` 中，继承的成员变量 `name`、`netPay` 和 `ssn` 可以通过名称访问，前提它们在基类 `Employee` 中标记为 `protected`（而不是 `private`）。对于任何不是派自基类的类，这些成员变量被视为标记为 `private`。

基类中为 `protected` 的成员变量在任何派生类中也表现为 `protected`。例如，假设你为 `HourlyEmployee` 定义了一个 `PartTimeHourlyEmployee` 类。`PartTimeHourlyEmployee` 类继承了 `HourlyEmployee` 类所有的成员变量，包括 `HourlyEmployee` 继承自 `Employee` 类的成员变量。`PartTimeHourlyEmployee` 类将拥有变量 `netPay`、`name` 和 `ssn`。如果这些成员变量在 `Employee` 类中标记为 `protected`，那么在 `PartTimeHourlyEmployee` 类的函数就可以可以通过名称使用它们。

# 第 14 章 继承

定义。然而，这并没有听起来那么糟糕。继承的私有成员变量可以通过调用读取或更改这些私有继承变量的继承函数来间接访问。对于是否应该使用 `protected` 成员，权威意见并不一致，你必须根据自己的判断决定是否利用它们。

## 保护成员 (Protected Members)

如果你在类成员之前使用限定保护访问符（而不是 `private` 或 `public`），那么对于派生类以外的任何类或函数，其效果与成员变量被标记为 `private` 相同。然而，在派生类成员函数的定义中，可以通过名称访问该变量。同样，如果你在类成员函数或派生类以外的函数之前使用限定保护访问符，其效果与成员变量被标记为 `private` 相同。然而，在派生类成员函数的定义中，可以使用该保护函数。

保护成员在派生类中的继承方式，就像它们在派生类中是 `protected` 一样。换句话说，如果成员在基类中被标记为 `protected`，那么在所有后代类的定义中都可以通过名称访问，而不仅仅是在直接派自基类的类中。

## 自测练习 (Self-Test Exercises)

- 1. 下面程序是否合法（假设已添加适当的 `#include` 和 `using` 指令）？

```cpp
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

### 自测练习（续）

2. 为 `SmartBut` 类给出一个定义，它是下面给基类 `Smart` 的派生类。不需要考虑 `#include` 指令或命名空间细节。

```cpp
class Smart
{
public:
    Smart();
    void printAnswer() const;
protected:
    int a;
    int b;
}
```

该类应该有一个额外的数据字段 `crazy`，类型为 `bool`；一个不带参数并返回 `bool` 类型值的成员函数；合适的构造函数。该函数名为 `isCrazy`。你不需要提供任何实现，只需要类定义。

3. 这是否是自测练习 2 中讨论的派生类 `SmartBut` 中成员函数 `isCrazy` 的合法定义？请解释你的答案。（记住，问题问的是是否合法，而不是是否是一个合理的定义。）

```cpp
bool SmartBut::isCrazy() const
{
    if (a > b)
        return crazy;
    else
        return true;
}
```

## 成员函数的重定义 (Redefinition of Member Functions)

在派生类 `HourlyEmployee` 的定义（显示 14.3）中，我们给新成员函数 `setRate`、`getRate`、`setHours` 和 `getHours` 声明。我们还只为继承自 `Employee` 类的成员函数之一提供了函数声明。那些没有给出声明的继承成员函数（如 `setName` 和 `setName`）将被原封不动地继承。它们在 `HourlyEmployee` 类中的定义与在基类中的定义相同。当你定义派生类 `HourlyEmployee` 时，你只需要列出你想要在派生类中具有不同定义的继承函数的函数声明。如果你查看类 `HourlyEmployee` 类的实现（显示 14.5），你会发现我们重定义了继承的成员函数 `printCheck`。`SalariedEmployee` 类也为成员函数 `printCheck` 提供了一个新定义，如显示 14.6 所示。此外，这两个类给出的定义是不同的。函数 `printCheck` 在派生类中被重定义。

## 第 14 章 继承 (CHAPTER 14 Inheritance)

显示 14.7 提供了一个演示程序，阐述了派生类 `HourlyEmployee` 和 `SalariedEmployee` 的用法。

## 重定义继承的函数 (Redefining an Inherited Function)

派生类继承属于基类的所有成员函数（和成员变量）。然而，如果派生类对继承的成员函数需要不同的实现，则可以在派生类中重定义该函数。当成员函数被重定义时，你必须在派生类的定义中列出它的声明，即使该声明与基类中的声明相同。如果你不想重定义继承自基类的成员函数，则不要在派生类的定义中列出它。

## 重定义与重载 (Redefining versus Overloading)

不要将在派生类中重定义函数与重载函数名混淆。当你重定义一个函数定义时，在派生类中给出的新定义具有相同数量和类型的参数。当你重载一个函数时，派生类中的函数与基类中的函数相比，具有不同数量的参数或不同类型的参数，派生类同时拥有这两个函数。例如，假设我们在 `HourlyEmployee` 类的定义中添加了一个带有以下函数声明的的函数：

```cpp
void setName(string firstName, string lastNameName);
```

那么 `HourlyEmployee` 类将拥有这个两个参数的函数 `setName`：

```cpp
void setName(string newName);
```

`HourlyEmployee` 类将有两个名为 `setName` 的函数。这就是对函数名 `setName` 的重载。

另一方面，`Employee` 类和 `HourlyEmployee` 类都定义了一个具有以下函数声明的函数：

```cpp
void printCheck();
```

另一方面，`Employee` 类和 `HourlyEmployee` 类都定义了一个具有以下函数声明的函数：

```cpp
void printCheck();
```
