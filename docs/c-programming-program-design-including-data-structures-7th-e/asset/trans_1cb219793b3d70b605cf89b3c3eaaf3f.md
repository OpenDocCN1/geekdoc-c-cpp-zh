
```cpp
clockType::clockType(int hours, int minutes, int seconds)
{
    if (0 <= hours && hours < 24)
        hr = hours;
    else
        hr = 0;

    if (0 <= minutes && minutes < 60)
        min = minutes;
    else
        min = 0;

    if (0 <= seconds && seconds < 60)
        sec = seconds;
    else
        sec = 0;
}
```

```cpp
clockType::clockType()  //default constructor
{
    hr = 0;
    min = 0;
    sec = 0;
}
```

从这些构造函数的定义可以看出，默认构造函数将三个成员变量——hr、min 和 sec——设置为0。此外，带参数的构造函数将成员变量设置为赋给形参的值。而且，我们可以通过调用函数 setTime 来编写带参数构造函数的定义，如下所示：

```cpp
clockType::clockType(int hours, int minutes, int seconds)
{
    setTime(hours, minutes, seconds);
}
```

## 调用构造函数

回想一下，当声明一个类对象时，构造函数会自动执行。因为一个类可能有多个构造函数，包括默认构造函数，接下来我们讨论如何调用特定的构造函数。

### 调用默认构造函数

假设一个类包含默认构造函数。调用默认构造函数的语法是：

```cpp
className classObjectName;
```

例如，语句：

```cpp
clockType yourClock;
```

声明 `yourClock` 为 `clockType` 类型的对象。在这种情况下，默认构造函数会执行，因为声明中不包含参数，并且 `yourClock` 的成员变量被初始化为0。

> **注意**
>
> 如果声明一个对象并希望执行默认构造函数，则在对象声明语句中，对象名后的空括号不是必需的。事实上，如果不小心包含了空括号，编译器会生成语法错误消息。例如，以下声明对象 `yourClock` 的语句是非法的：

```cpp
clockType yourClock();   //illegal object declaration
```

### 调用带参数的构造函数

假设一个类包含带参数的构造函数。调用带参数构造函数的语法是：

```cpp
className classObjectName(argument1, argument2, ...);
```

其中 argument1、argument2 等可以是变量或表达式。

注意以下事项：

- 实参的数量及其类型应与某个构造函数的形参（按给定顺序）匹配。
- 如果实参的类型与任何构造函数的形参（按给定顺序）都不匹配，C++ 会使用类型转换并寻找最佳匹配。例如，整数值可能被转换为小数部分为零的浮点值。任何歧义都会导致编译时错误。

考虑以下语句：

```cpp
clockType myClock(5, 12, 40);
```

这条语句声明了一个 `clockType` 类型的对象 `myClock`。这里，我们传递了三个 `int` 类型的值，它们与带参数构造函数的形参类型匹配。因此，类 `clockType` 的带参数构造函数会执行，并且对象 `myClock` 的三个成员变量被设置为5、12和40。

示例 10-6 进一步说明了构造函数如何执行。

## 示例 10-6

考虑以下类定义：

```cpp
class inventory
{
public:
    inventory();                         //Line 1
    inventory(string);                   //Line 2
    inventory(string, int, double);      //Line 3
    inventory(string, int, double, int); //Line 4

    //Add additional functions

private:
    string name;
    int itemNum;
    double price;
    int unitsInStock;
};
```

这个类有四个构造函数和四个成员变量。假设这些构造函数的定义如下：

```cpp
inventory::inventory() //default constructor
{
    name = "";
    itemNum = -1;
    price = 0.0;
    unitsInStock = 0;
}

inventory::inventory(string n)
{
    name = n;
    itemNum = -1;
    price = 0.0;
    unitsInStock = 0;
}

inventory::inventory(string n, int iNum, double cost)
{
    name = n;
    itemNum = iNum;
    price = cost;
    unitsInStock = 0;
}

inventory::inventory(string n, int iNum, double cost, int inStock)
{
    name = n;
    itemNum = iNum;
    price = cost;
    unitsInStock = inStock;
}
```

考虑以下声明：

```cpp
inventory item1;
inventory item2("Dryer");
inventory item3("Washer", 2345, 278.95);
inventory item4("Toaster", 8231, 34.49, 200);
```

对于 item1，第1行中的默认构造函数会执行，因为没有向该变量传递任何值。对于 item2，第2行中的构造函数会执行，因为只传递了一个 string 类型的参数，并且它与第2行中的构造函数匹配。对于 item3，第3行中的构造函数会执行，因为向 item3 传递了三个参数，并且它们与第3行中的构造函数匹配。类似地，对于 item4，第4行中的构造函数会执行（参见图 10-7）。

![](img/d0be7fc6d804b63484835c6c8bc67a07_724_0.png)

**图 10-7** 构造函数对对象的影响

> **注意：** 如果传递给类对象的值与任何构造函数的参数都不匹配，并且无法进行类型转换，则会生成编译时错误。

## 构造函数与默认参数

构造函数也可以有默认参数。在这种情况下，声明形参的规则与在函数中声明默认形参的规则相同。此外，传递给带默认参数构造函数的实参按照带默认参数函数的规则进行传递。（第6章讨论带默认参数的函数。）使用定义默认参数的规则，在 `class` clockType 的定义中，你可以将以下两个构造函数

```cpp
clockType(int, int, int);
clockType();
```

替换为以下语句。（回想一下，在函数原型中，形参的名称是可选的。）

```cpp
clockType(int = 0, int = 0, int = 0);    //Line 1
```

在实现文件中，这个构造函数的定义与带参数构造函数的定义相同。

如果用第1行中的构造函数（带默认参数的构造函数）替换 `class` clockType 的构造函数，那么可以如下声明具有零个、一个、两个或三个实参的 clockType 对象：

```cpp
clockType clock1;                 //Line 2
clockType clock2(5);               //Line 3
clockType clock3(12, 30);          //Line 4
clockType clock4(7, 34, 18);       //Line 5
```

clock1 的成员变量被初始化为0。clock2 的成员变量 hr 被初始化为5，clock2 的成员变量 min 和 sec 被初始化为0。clock3 的成员变量 hr 被初始化为12，clock3 的成员变量 min 被初始化为30，clock3 的成员变量 sec 被初始化为0。clock4 的成员变量 hr 被初始化为7，clock4 的成员变量 min 被初始化为34，clock4 的成员变量 sec 被初始化为0。

使用这些约定，我们可以说，没有参数或所有参数都是默认参数的构造函数称为**默认构造函数**。

## 类与构造函数：注意事项

如前一部分所述，构造函数提供对象成员变量的有保证的初始化。通常，默认构造函数用于将成员变量初始化为某些默认值，并且该构造函数没有参数。带参数的构造函数用于将成员变量初始化为某些特定值。

我们已经看到，如果一个类没有构造函数，那么创建的对象是未初始化的，因为 C++ 在声明变量时不会自动初始化变量。实际上，如果一个类没有构造函数，那么 C++ 会自动提供默认构造函数。然而，这个默认构造函数*不会*初始化正在声明的对象。
