

接下来，让我们编写 `class clockType` 成员函数的定义。也就是说，我们将编写函数 `setTime`、`getTime`、`printTime`、`incrementSeconds`、`equalTime` 等的定义。由于标识符 `setTime`、`printTime` 等是类私有的，我们不能在类外部（直接）引用它们。为了引用这些标识符，我们使用**作用域解析运算符** `::`（双冒号）。在函数定义的头行中，函数名由类名、作用域解析运算符和函数名依次组成。例如，函数 `setTime` 的定义如下：

```cpp
void clockType::setTime(int hours, int minutes, int seconds)
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

注意，函数 `setTime` 的定义检查了 `hours`、`minutes` 和 `seconds` 的合法性。如果这些值超出范围，成员变量 `hr`、`min` 和 `sec` 将被初始化为 0。现在让我们解释成员函数 `setTime` 在由 `clockType` 类型的对象访问时是如何工作的。

成员函数 `setTime` 是一个 void 函数，并且有三个参数。因此：

-   对这个函数的调用是一个独立的语句。
-   在调用这个函数时，我们必须使用三个参数。

此外，回想一下，由于 `setTime` 是 `class clockType` 的成员，它可以直接访问成员变量 `hr`、`min` 和 `sec`，如 `setTime` 的定义所示。

假设 `myClock` 是一个 `clockType` 类型的对象（如前所述）。对象 `myClock` 有三个成员变量，如图 10-4(a) 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_712_0.png)

考虑下面的语句：

```cpp
myClock.setTime(3, 48, 52);
```

现在函数 `setTime` 被调用，参数为 3、48 和 52。因此，函数 `setTime` 的形参 `hours`、`minutes` 和 `seconds` 的值分别为 3、48 和 52。接下来，在语句 `myClock.setTime(3, 48, 52);` 中，`setTime` 由对象 `myClock` 访问。因此，函数 `setTime` 函数体中所引用的三个变量——`hr`、`min` 和 `sec`——就是 `myClock` 的三个成员变量。当函数 `setTime` 的函数体执行时，`hours` 的值被复制到 `myClock.hr`，`minutes` 的值被复制到 `myClock.min`，`seconds` 的值被复制到 `myClock.sec`。本质上，前面语句中作为参数传递的值 3、48 和 52，由函数 `setTime` 赋值给 `myClock` 的三个成员变量（参见函数 `setTime` 的函数体）。在前面的语句执行后，对象 `myClock` 如图 10-4(b) 所示。

接下来，让我们给出 `class clockType` 的其他成员函数的定义。这些函数的定义简单且易于理解：

```cpp
void clockType::getTime(int& hours, int& minutes,
                        int& seconds) const
{
    hours = hr;
    minutes = min;
    seconds = sec;
}

void clockType::printTime() const
{
    if (hr < 10)
        cout << "0";
    cout << hr << ":";

    if (min < 10)
        cout << "0";
    cout << min << ":";

    if (sec < 10)
        cout << "0";
    cout << sec;
}

void clockType::incrementHours()
{
    hr++;
    if (hr > 23)
        hr = 0;
}

void clockType::incrementMinutes()
{
    min++;
    if (min > 59)
    {
        min = 0;
        incrementHours();
    }
}

void clockType::incrementSeconds()
{
    sec++;

    if (sec > 59)
    {
        sec = 0;
        incrementMinutes();
    }
}
```

从函数 `incrementMinutes` 和 `incrementSeconds` 的定义可以清楚地看出，类的成员函数可以调用该类的其他成员函数。

函数 `equalTime` 的定义如下：

```cpp
bool clockType::equalTime(const clockType& otherClock) const
{
    return (hr == otherClock.hr
            && min == otherClock.min
            && sec == otherClock.sec);
}
```

让我们看看成员函数 `equalTime` 是如何工作的。

假设 `myClock` 和 `yourClock` 是 `clockType` 类型的对象，如前所述。进一步假设 `myClock` 和 `yourClock` 如图 10-5 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_714_0.png)

图 10-5 对象 myClock 和 yourClock

考虑下面的语句：

```cpp
if (myClock.equalTime(yourClock))
.
.
.
```

在表达式：

```cpp
myClock.equalTime(yourClock)
```

中，对象 `myClock` 访问成员函数 `equalTime`。由于 `otherClock` 是一个引用参数，实参 `yourClock` 的地址被传递给形参 `otherClock`，如图 10-6 所示。

![](img/b217c421655b51e7494cf3b89bb5432d_714_1.png)

图 10-6 对象 myClock 和参数 otherClock

`otherClock` 的成员变量 `hr`、`min` 和 `sec` 的值分别为 14、25 和 54。换句话说，当函数 `equalTime` 的函数体执行时，`otherClock.hr` 的值为 14，`otherClock.min` 的值为 25，`otherClock.sec` 的值为 54。函数 `equalTime` 是 `myClock` 的一个成员。当函数 `equalTime` 执行时，函数 `equalTime` 函数体中的变量 `hr`、`min` 和 `sec` 是对象 `myClock` 的成员变量。因此，`myClock` 的成员 `hr` 与 `otherClock.hr` 比较，`myClock` 的成员 `min` 与 `otherClock.min` 比较，`myClock` 的成员 `sec` 与 `otherClock.sec` 比较。

同样，从函数 `equalTime` 的定义可以清楚地看出为什么它只有一个参数。

让我们再看一下函数 `equalTime` 的定义。注意，在这个函数的定义中，对象 `otherClock` 访问了成员变量 `hr`、`min` 和 `sec`。然而，这些成员变量是私有的。那么，这是否违反访问规则？答案是否定的。函数 `equalTime` 是 `class clockType` 的一个成员，而 `hr`、`min` 和 `sec` 是成员变量。此外，`otherClock` 是 `clockType` 类型的对象。因此，对象 `otherClock` 可以在函数 `equalTime` 的定义中访问它自己的私有成员变量。

对于类的任何成员函数也是如此。一般来说，当你编写一个类的成员函数（例如 `dummyFunction`）的定义时，假设该类为 `dummyClass`，并且该函数使用了该 `dummyClass` 类的一个对象 `dummyObject`，那么在 `dummyFunction` 的定义中，对象 `dummyObject` 可以访问它自己的私有成员变量（实际上，是该类的任何私有成员）。

一旦一个类被正确定义和实现，它就可以在程序中使用。使用并操作类的对象的程序或软件被称为该类的客户端。

当你声明 `clockType` 类的对象时，每个对象都有自己的一份成员变量 `hr`、`min` 和 `sec` 的副本。在面向对象的术语中，像 `hr`、`min` 和 `sec` 这样的变量被称为类的实例变量，因为每个对象实例都有自己的一份数据副本。

## 访问器函数和修改器函数

让我们看一下 `clockType` 类的成员函数。函数 `setTime` 将成员变量的值设置为用户指定的值。换句话说，它改变或修改了成员变量的值。同样，函数 `incrementSeconds`、`incrementMinutes` 和 `incrementHours` 也修改了成员变量。另一方面，像 `getTime`、`printTime` 和 `equalTime` 这样的函数只访问成员变量的值，并不修改成员变量。因此，我们可以将 `clockType` 类的成员函数分为两类：修改成员变量的成员函数和仅访问但不修改成员变量的成员函数。

这对于任何类来说通常都是如此。也就是说，每个类都有仅访问但不修改成员变量的成员函数，称为访问器函数，以及修改成员变量的成员函数，称为修改器函数。

**访问器函数：** 类的仅访问（即不修改）成员变量值的成员函数。

**修改器函数：** 类的修改成员变量值的成员函数。

由于访问器函数只访问成员变量的值，作为一种安全措施，我们通常会在函数头部的末尾加上保留字 `const`。

