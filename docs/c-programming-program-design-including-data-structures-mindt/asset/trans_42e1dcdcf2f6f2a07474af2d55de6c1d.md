

构造函数具有以下性质：

- 构造函数的名字与类名相同。
- 构造函数是一个函数，但它没有类型。也就是说，它既不是返回值的函数，也不是 void 函数。
- 一个类可以有多个构造函数。但是，一个类的所有构造函数都具有相同的名字。
- 如果一个类有多个构造函数，那么这些构造函数的形参列表必须不同。也就是说，要么形参个数不同；要么形参个数相同，但按顺序排列的形参数据类型至少有一个位置不同。换句话说，与函数重载类似，构造函数的名字是被重载的。
- 当类对象被声明并进入其作用域时，构造函数会自动执行。由于它们没有类型，不能像其他函数那样被调用。
- 执行哪个构造函数取决于声明类对象时传递给该类对象的值的类型。

让我们扩展 `clockType` 类的定义，加入两个构造函数：

```cpp
class clockType
{
public:
    void setTime(int, int, int);
    void getTime(int&, int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;
    clockType(int, int, int);  //带参数的构造函数
    clockType();  //默认构造函数

private:
    int hr;
    int min;
    int sec;
};
```

`clockType` 类的这个定义包含两个构造函数：一个带三个参数，一个不带任何参数。现在让我们编写这些构造函数的定义：

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
clockType::clockType()  //默认构造函数
{
    hr = 0;
    min = 0;
    sec = 0;
}
```

从这些构造函数的定义可以看出，默认构造函数将三个成员变量——hr、min 和 sec——设置为 0。此外，带参数的构造函数将成员变量设置为赋给形参的任何值。而且，我们可以通过调用 `setTime` 函数来编写带参数的构造函数的定义，如下所示：

```cpp
clockType::clockType(int hours, int minutes, int seconds)
{
    setTime(hours, minutes, seconds);
}
```

## 调用构造函数

回顾一下，当声明类对象时，构造函数会被自动执行。因为一个类可能有多个构造函数，包括默认构造函数，接下来我们讨论如何调用特定的构造函数。

### 调用默认构造函数

假设一个类包含默认构造函数。调用默认构造函数的语法是：

```cpp
className classObjectName;
```

例如，语句：

```cpp
clockType yourClock;
```

将 `yourClock` 声明为 `clockType` 类型的对象。在这种情况下，由于声明中没有包含参数，默认构造函数会执行，`yourClock` 的成员变量被初始化为 0。

> **注意**
>
> 如果你声明一个对象并希望执行默认构造函数，对象声明语句中不需要在对象名后面加空括号。事实上，如果你不小心加上了空括号，编译器会生成一条语法错误信息。例如，下面声明对象 `yourClock` 的语句是非法的：
>
> ```cpp
> clockType yourClock(); //非法的对象声明
> ```

### 调用带参数的构造函数

假设一个类包含带参数的构造函数。调用带参数的构造函数的语法是：

```cpp
className classObjectName(argument1, argument2, ...);
```

其中 `argument1`、`argument2` 等可以是变量或表达式。

请注意以下几点：

- 参数的数量和类型应与某个构造函数的形参（按给定顺序）匹配。
- 如果参数的类型与任何构造函数的形参（按给定顺序）都不匹配，C++ 会使用类型转换并寻找最佳匹配。例如，整数值可能被转换为小数部分为零的浮点值。任何歧义都会导致编译时错误。

考虑语句：

```cpp
clockType myClock(5, 12, 40);
```

该语句声明了一个 `clockType` 类型的对象 `myClock`。这里，我们传入了三个 `int` 类型的值，这与带参数的构造函数的形参类型相匹配。因此，`clockType` 类中带参数的构造函数会执行，对象 `myClock` 的三个成员变量被设置为 5、12 和 40。

示例 10-6 进一步说明了构造函数是如何执行的。

### 示例 10-6

考虑以下类定义：

```cpp
class inventory
{
public:
    inventory();                         //第1行
    inventory(string);                   //第2行
    inventory(string, int, double);      //第3行
    inventory(string, int, double, int); //第4行

    //添加其他函数

private:
    string name;
    int itemNum;
    double price;
    int unitsInStock;
};
```

这个类有四个构造函数和四个成员变量。假设构造函数的定义如下：

```cpp
inventory::inventory() //默认构造函数
{
    name = "";
    itemNum = -1;
    price = 0.0;
    unitsInStock = 0;
}
```

```cpp
inventory::inventory(string n)
{
    name = n;
    itemNum = -1;
    price = 0.0;
    unitsInStock = 0;
}
```

```cpp
inventory::inventory(string n, int iNum, double cost)
{
    name = n;
    itemNum = iNum;
    price = cost;
    unitsInStock = 0;
}
```

```cpp
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

对于 `item1`，由于没有向该变量传递任何值，第 1 行的默认构造函数会执行。对于 `item2`，由于只传递了一个 `string` 类型的参数，并且它与第 2 行的构造函数匹配，因此第 2 行的构造函数会执行。对于 `item3`，由于向 `item3` 传递了三个参数，并且它们与第 3 行的构造函数匹配，因此第 3 行的构造函数会执行。类似地，对于 `item4`，第 4 行的构造函数会执行（参见图 10-7）。

![](img/b217c421655b51e7494cf3b89bb5432d_725_0.png)

图 10-7  构造函数对对象的影响

> **注意**
>
> 如果传递给类对象的值与任何构造函数的参数都不匹配，并且无法进行类型转换，则会生成编译时错误。

## 构造函数与默认参数

构造函数也可以有默认参数。在这种情况下，声明形参的规则与在函数中声明默认形参的规则相同。此外，向具有默认参数的构造函数传递实际参数时，遵循向具有默认参数的函数传递参数的规则。（第 6 章讨论了具有默认参数的函数。）利用定义默认参数的规则，在 `clockType` 类的定义中，你可以用下面的语句替换两个构造函数

```cpp
clockType(int, int, int);
clockType();
```

（回想一下，在函数原型中，形参的名字是可选的。）

```cpp
clockType(int = 0, int = 0, int = 0);  //第1行
```

在实现文件中，这个构造函数的定义与带参数的构造函数的定义相同。

如果你用第 1 行中的构造函数（带默认参数的构造函数）替换 `clockType` 类的构造函数，那么你可以用零个、一个、两个或三个参数来声明 `clockType` 对象，如下所示：

```cpp
clockType clock1;                 //第2行
clockType clock2(5);              //第3行
clockType clock3(12, 30);         //第4行
clockType clock4(7, 34, 18);      //第5行
```

`clock1` 的成员变量被初始化为 0。`clock2` 的成员变量 `hr` 被初始化为 5，成员变量 `min` 和 `sec` 被初始化为 0。`clock3` 的成员变量 `hr` 被初始化为 12，成员变量 `min` 被初始化为 30，成员变量 `sec` 被初始化为 0。`clock4` 的成员变量 `hr` 被初始化为 7，成员变量 `min` 被初始化为 34，成员变量 `sec` 被初始化为 18。

使用这些约定，我们可以说，没有参数或所有参数都有默认值的构造函数被称为**默认构造函数**。

## 类与构造函数：一个注意事项

如前文所述，构造函数提供了对对象成员变量的有保证的初始化。通常，默认构造函数用于将成员变量初始化为某些默认值，并且该构造函数没有参数。带参数的构造函数用于将成员变量初始化为某些特定值。

我们已经看到，如果一个类没有构造函数，那么创建的对象是未初始化的，因为 C++ 在声明变量时不会自动初始化变量。实际上，如果一个类没有构造函数，C++ 会自动提供默认构造函数。但是，这个默认构造函数**不会**初始化所声明的对象。

