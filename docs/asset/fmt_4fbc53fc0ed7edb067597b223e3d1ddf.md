
```cpp
int main() {

    clockType myClock; //第1行

    clockType yourClock; ////第2行

                         //第3行

                         //第4行

    int hours;

    int minutes;

    int seconds;

    // 设置 myClock 的时间
    myClock.setTime(5, 4, 30);

    cout << "Line 9: myClock:";
    myClock.printTime(); //打印 myClock 的时间
    cout << endl;

    cout << "Line 12: yourClock: ";
    yourClock.printTime(); //打印 yourClock 的时间
    cout << endl;

    // 设置 yourClock 的时间
    yourClock.setTime(5, 45, 16);

    cout << "Line 16: After setting, yourClock: ";
    yourClock.printTime(); //打印 yourClock 的时间
    cout << endl;

    // 比较 myClock 和 yourClock
    if (myClock.equalTime(yourClock)) {
        cout << "Line 20: Both times are equal.";
    } else {
        cout << "Line 22: The times are not equal.";
    }

    cout << endl;

    cout << "Line 23: Enter the hours, ";
    cin >> hours >> minutes >> seconds;

    // 使用变量设置 myClock 的时间
    myClock.setTime(hours, minutes, seconds);

    cout << "Line 27: New myClock:";
    myClock.printTime();
    cout << endl;

    // 将 myClock 的时间增加一秒
    myClock.incrementSeconds();

    cout << "Line 31: After incrementing myClock, ";
    myClock.printTime();
    cout << endl;

    // 使用变量获取 yourClock 的值
    yourClock.getTime(hours, minutes);

    cout << "Line 35: hours = " << hours << ", minutes = " << minutes << ", seconds = " << seconds;
    cout << endl;

    return 0;
}
```

```cpp
void clockType::setTime(int hours, int minutes, int seconds) {
    if (0 <= hours < 24)
        hr = hours;
    } else {
        hr = 0;
    }

    if (0 <= minutes < 60)
        min = minutes;
    } else {
        min = 0;
    }

    if (0 <= seconds < 60)
        sec = seconds;
    } else {
        sec = 0;
    }
}
```

```cpp
public:
void setTime(int, int, int);
void getTime(int&, int&) const;
void printTime() const;
void incrementSeconds();
void incrementMinutes();
void incrementHours();
bool equalTime(const clockType&) const;
```

# 示例 10-5

```cpp
class clockType {
    int hr;
    int min;
    int sec;
public:
    void setTime(int, int, int);
    void getTime(int&, int&) const;
    void printTime() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&) const;
}
```

在示例 10-5 中，由于标识符 `hr`、`min` 和 `sec` 没有任何访问修饰符，因此它们默认是私有的（private）。

通常的做法是先列出公共成员，然后列出私有成员。这样你可以将注意力放在公共成员上。

# 构造函数

在程序示例 10-2 中，当我们调用 `setTime` 函数打印 `yourClock` 的值时，输出是一些奇怪的数字（示例运行中第 5 行的输出）。这是由于 C++ 不会自动初始化变量。由于类的私有成员无法在类外部访问（在本例中，为成员变量），如果用户尝试通过调用 `setTime` 函数来初始化这些变量，程序将产生错误的结果。

为了保证类的成员变量被初始化，你使用构造函数。构造函数有两种类型：带参数和不带参数。不带参数的构造函数被称为默认构造函数。

# 672 | 第 10 章：类与数据抽象

构造函数具有以下属性：

- 构造函数的名称与类名相同。
- 构造函数是一个没有值的函数且没有类型。也就是说，它既不是返回值的函数，也不是 `void` 函数。
- 一个类可以有多个构造函数。然而，一个类的所有构造函数具有相同的名称。
- 如果一个类有多个构造函数，则这些构造函数必须具有不同的形式参数列表；或者，如果形式参数的数量相同，那么按照列出的顺序，形式参数的数据类型在至少一个位置上不同。也就是说，就像函数重载一样，构造函数的名称也是重载的。
- 当类对象被声明并进入其作用域时，构造函数会自动执行。因为它们没有类型，所以不能像其他函数那样被调用。
- 执行哪一个构造函数取决于声明类时传递给类对象的值类型。

让我们通过包含两个构造函数来扩展 `class clockType` 的定义：

```cpp
class clockType
public:
    void setState(int, int, int);
    void getTime(int&, int&, int&) const;
    void print() const;
    void incrementSeconds();
    void incrementMinutes();
    void incrementHours();
    bool equalTime(const clockType&);
    clockType(int, int, int); // 带参数的构造函数
    clockType(); // 默认构造函数
private:
    int hr;
    int min;
    int sec;
```

这个 `class clockType` 的定义包含了两个构造函数：一个带三个参数，一个没有任何参数。现在我们来编写这些构造函数的定义：

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
clockType::clockType() // 默认构造函数
{
    hr = 0;
    min = 0;
    sec = 0;
}
```

从这些构造函数的定义可以得出，默认构造函数将三个成员变量——`hr`、`min` 和 `sec`设置为 0。此外，带参数的构造函数将成员变量设置为赋值给形式参数的值。此外，我们可以通过调用 `setTime` 函数来编写带参数构造函数的定义，如下：

```cpp
clockType::clockType(int hours, int minutes, int seconds)
{
    setTime(hours, minutes, seconds);
}
```

# 调用构造函数

记住，当声明类对象时，构造函数会自动执行。由于一个类可能有多个构造函数（包括默认构造函数），我们将讨论如何调用特定的构造函数。

# 调用默认构造函数

假设一个类包含默认构造函数。调用默认构造函数的语法为：

```cpp
className classObjectName;
```

例如，语句：

```cpp
clockType yourClock;
```

声明 `yourClock` 为 `clockType` 类型的对象。在这种情况下，由于声明中没有包含参数，因此执行默认构造函数，`yourClock` 的成员变量被初始化为0。

注意 如果你声明一个对象并执行默认构造函数，在对象声明中对象名称后面不需要空括号。事实上，如果你不小心包含了空括号，编译器会生成语法错误信息。例如，以下声明对象 `yourClock` 的语句是非合法的：`clockType yourClock(); //非法对象`

# 调用带参数的构造函数

假设一个类包含带参数的构造函数。调用带参数构造函数的语法为：

```cpp
className classObjectName(argument1, argument2, ...);
```

注意以下：

- 传递给类对象的参数数量必须与构造函数匹配。
- 参数的类型必须与形式参数匹配，或者可以转换为它们。
- 如果有多个构造函数可以匹配，编译器将选择最匹配的一个。

例如，语句：

```cpp
clockType yourClock(5, 12, 30);
```

声明了 `clockType` 类型。这里传递了三个值，与该构造函数匹配。

# 示例 10-6

示例 10-6 展示了构造函数是如何执行的。考虑以下类：

```cpp
class inventory {
public:
    inventory(); // 第1行
    inventory(string); // 第2行
    inventory(string, int, double); // 第3行
    inventory(string, int, double, int); // 第4行
private:
    string name;
    int itemNum;
    double price;
    int unitsStock;
};
```

该类有四个构造函数。假设构造函数的定义如下：

```cpp
inventory::inventory() {
    name = "";
    itemNum = -1;
    price = 0.0;
    unitsStock = 0;
}
```

```cpp
inventory::inventory(string n) {
    name = n;
    itemNum = -1;
    price = 0.0;
    unitsStock = 0;
}
```

```cpp
inventory::inventory(string n, int iNum, double cost) {
    name = n;
    itemNum = iNum;
    price = cost;
    unitsStock = 0;
}
```

```cpp
inventory::inventory(string n, int iNum, double cost, int inStock) {
    name = n;
    itemNum = iNum;
    price = cost;
    unitsStock = inStock;
}
```

考虑以下声明：

```cpp
inventory item1;
inventory item2("Dryer");
inventory item3("Washer", 2345, 278.95);
inventory item4("Toaster", 8231, 34.49, 200);
```

对于 `item1`，执行第1行的构造函数，因为没有向此变量传递。对于 `item2`，执行第2行的构造函数，因为传递了一个类型为 `string` 的参数，它与第2行的构造函数匹配。对于 `item3`，执行第3行的构造函数，因为传递给 `item3` 三个参数，它们与第3行的构造函数匹配。同样，对于 `item4`，执行第4行的构造函数（见图10-7）。

![](img/d998292a174f7bfd8a26bfbada3d454e_725_0.png)

图10-7 构造函数对对象的影响

注意 如果传递给类对象的值不匹配任何构造函数的参数且不存在可能的类型转换，将产生编译时错误。

# 构造函数与默认参数

构造函数也可以具有默认参数。在这种情况下，声明形式参数的规则与在函数中声明形式参数的规则相同。此外，传递带有默认参数的构造函数的实际参数是按照带有默认参数函数的规则传递的。（第 6 章讨论了带有默认参数的构造函数。）使用定义默认参数的规则，在 `clockType` 类的定义中，你可以替换两个构造函数：

```
clockType(int, int, int);
clockType();
```

使用以下语句（记住在函数原型中，参数名称是可选的）。

```
clockType(int = 0, int = 0, int = 0); //Line 1
```

在实现文件中，该构造函数的定义与带参数的构造函数的定义相同。

如果你将类 `clockType` 的构造函数替换为带有默认参数的构造函数，你可以如下声明具有零、一个或三个参数的 `clockType` 对象：

```
clockType clock1; //Line 2
clockType clock2(5); //Line 3
clockType clock3(12, 30); //Line 4
clockType clock4(7, 34, 18); //Line 5
```

`clock1` 的成员被初始化为 0。`clock2` 的成员变量 `hr` 初始化为 5，`clock2` 的成员变量 `min` 初始化为 0。`clock3` 的成员变量 `hr` 初始化为 30，`clock3` 的成员变量 `sec` 初始化为 0。`clock4` 的成员变量 `hr` 初始化为 7，`clock4` 的成员变量 `min` 初始化为 34，`clock4` 的成员变量 `sec` 初始化为 18。

根据这些约定，我们可以说，没有参数或全为默认参数的构造函数被称为**默认构造函数**。

# 类与构造函数：注意事项

在前节中，构造函数保证了对象成员变量的初始化。通常，使用默认构造函数将成员变量初始化为某些默认值，这种构造函数没有参数。带参数的构造函数用于将成员变量初始化为某些特定值。

我们已经看到如果一个类没有构造函数，那么对象是未定义的，因为 C++ 在声明变量时不会进行初始化。实际上，如果一个类没有构造函数，C++ 会自动提供默认构造函数。然而，这个默认构造函数**并不会**初始化正在声明的对象。

关于类和构造函数需要记住的重要点如下：

- 如果一个类没有构造函数，C++ 会自动提供默认构造函数。然而，声明的对象仍然是未定义的。
- 另一方面，假设一个类（例如 `dummyClass`）包含了带参数的构造函数且不包含默认构造函数。在这种情况下，C++ 不为 `dummyClass` 类提供默认构造函数。因此，当声明 `dummyClass` 类的对象时，我们必须在声明中包含适当的参数。

以下代码进一步解释了这一点。考虑以下类的定义：

```
class dummyClass {
public:
    void print() const;
    dummyClass(int dx, int dy);
private:
    int x;
    int y;
};
```

`dummyClass` 类有一个带参数的构造函数。它没有为它编写默认构造函数，且 C++ 不会自动提供，因为至少已经为它写了一个构造函数。根据这个 `dummyClass` 类的定义，以下对象声明是：

```
dummyClass dummyObject(10, 25); //对象声明是合法的
```

因为类 `dummyClass` 不包含默认构造函数，以下声明是错误的并且会产生语法错误：

```
dummyClass dummyObject; //错误的对象声明
```
