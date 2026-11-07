
接下来，新的 `fill()` 应如下所示：

```cpp
void fill(std::array<double, Seasons>& pa)   // changed
{
    using namespace std;
    for (int i = 0; i < Seasons; i++)
    {
        cout << "Enter " << Snames[i] << " expenses: ";
        cin >> pa[i];   // changed
    }
}
```

注意，`(*pa)[i]` 改成了更简单的 `pa[i]`。

最后，对 `show()` 的唯一改动是函数头：

```cpp
void show(std::array<double, Seasons>& da)
```

### 6.
a. 可以通过为第二个参数使用默认值来实现：

```cpp
double mass(double d, double v = 1.0);
```

也可以通过使用函数重载来实现：

```cpp
double mass(double d, double v);
double mass(double d);
```

b. 不能为重复值使用默认值，因为必须从右到左提供默认值。可以使用重载：

```cpp
void repeat(int times, const char* str);
void repeat(const char* str);
```

c. 可以使用函数重载：

```cpp
int average(int a, int b);
double average(double x, double y);
```

d. 不能这样做，因为两个版本会有相同的签名。

### 7.

```cpp
template<class T>
T max(T t1, T t2)   // or T max(const T& t1, const T& t2)
{
    return t1 > t2 ? t1 : t2;
}
```

### 8.

```cpp
template<> box max(box b1, box b2)
{
    return b1.volume > b2.volume ? b1 : b2;
}
```

### 9.

`v1` 的类型是 `float`，`v2` 的类型是 `float&`，`v3` 的类型是 `float&`，`v4` 的类型是 `int`，`v5` 的类型是 `double`。字面量 `2.0` 的类型是 `double`，所以乘积 `2.0 * m` 的类型是 `double`。

## 第9章复习题答案

### 1.
a. `homer` 自动成为自动变量。

b. `secret` 应在一个文件中定义为外部变量，并在第二个文件中使用 `extern` 声明。

c. `topsecret` 可以通过在外部定义前加上关键字 `static`，定义为具有内部链接的静态变量。或者可以将其定义在未命名命名空间中。

d. `beencalled` 应通过在函数中的声明前加上关键字 `static`，定义为局部静态变量。

### 2.

using 声明使命名空间中的单个名称可用，其作用域对应于该 using 声明所在的声明区域。using 指令使命名空间中的所有名称可用。使用 using 指令时，就好像在同时包含该 using 声明和命名空间本身的最小声明区域中声明了这些名称。

### 3.

```cpp
#include <iostream>
int main()
{
    double x;
    std::cout << "Enter value: ";
    while (!(std::cin >> x))
    {
        std::cout << "Bad input. Please enter a number: ";
        std::cin.clear();
        while (std::cin.get() != '\n')
            continue;
    }
    std::cout << "Value = " << x << std::endl;
    return 0;
}
```

### 4.

以下是修改后的代码：

```cpp
#include <iostream>
int main()
{
    using std::cin;
    using std::cout;
    using std::endl;

    double x;
    cout << "Enter value: ";
    while (!(cin >> x))
    {
        cout << "Bad input. Please enter a number: ";
        cin.clear();
        while (cin.get() != '\n')
            continue;
    }
    cout << "Value = " << x << endl;
    return 0;
}
```

### 5.

可以在每个文件中分别定义静态函数。或者每个文件都可以在未命名命名空间中定义相应的 `average()` 函数。

### 6.

```text
10
4
0
Other: 10, 1
another(): 10, -4
```

### 7.

```text
1
4, 1, 2
2
2
4, 1, 2
2
```

## 第10章复习题答案

### 1.

类是对用户定义类型的定义。类声明指定数据如何存储，并指定可用于访问和操作该数据的方法（类成员函数）。

### 2.

类通过类方法的公共接口表示可以对类对象执行的操作；这就是抽象。类可以对数据成员使用私有可见性（默认），这意味着只能通过成员函数访问数据；这就是数据隐藏。实现细节（如数据表示和方法代码）被隐藏；这就是封装。

### 3.

类定义一种类型，包括如何使用它。对象是变量或其他数据对象，例如由 `new` 生成的对象，它根据类定义创建和使用。类与对象之间的关系，同标准类型与该类型的变量之间的关系相同。

### 4.

如果创建给定类的多个对象，每个对象都有用于自己数据集的存储空间。但所有对象共用同一组成员函数。（通常，方法是公有的，数据成员是私有的，但这是策略问题，而不是类的要求。）

### 5.

此示例使用 char 数组保存字符数据，但也可以改用 `string` 类对象。

```cpp
// #include <cstring>

// class definition
class BankAccount
{
private:
    char name[40];      // or std::string name;
    char acctnum[25];   // or std::string acctnum;
    double balance;
public:
    BankAccount(const char* client, const char* num, double bal = 0.0);
// or BankAccount(const std::string& client,
//                const std::string& num, double bal = 0.0);

    void show(void) const;
    void deposit(double cash);
    void withdraw(double cash);
};
```

### 6.

创建该类的对象时，或显式调用构造函数时，会调用类构造函数。对象过期时，会调用类析构函数。

### 7.

以下是两种可能的解决方案（注意，必须包含 `cstring` 或 `string.h` 才能使用 `strncpy()`，否则必须包含 `string` 才能使用 string 类）：

```cpp
BankAccount::BankAccount(const char* client, const char* num, double bal)
{
    strncpy(name, client, 39);
    name[39] = '\0';
    strncpy(acctnum, num, 24);
    acctnum[24] = '\0';
    balance = bal;
}
```

或者

```cpp
BankAccount::BankAccount(const std::string& client,
                         const std::string& num, double bal)
{
    name = client;
    acctnum = num;
    balance = bal;
}
```

请记住，默认参数放在原型中，而不是函数定义中。

### 8.

默认构造函数要么没有参数，要么为所有参数提供默认值。拥有默认构造函数使你能够声明对象而不初始化它们，即使已经定义了初始化构造函数。它还允许声明数组。

### 9.

```cpp
// stock3.0.h
#ifndef STOCK3_0_H_
#define STOCK3_0_H_

class Stock
{
    private:
        std::string company;
        long shares;
        double share_val;
        double total_val;
        void set_tot() { total_val = shares * share_val; }
    public:
        Stock();             // default constructor
        Stock(const std::string& co, long n, double pr);
        ~Stock() { }         // do-nothing destructor
        void buy(long num, double price);
        void sell(long num, double price);
        void update(double price);
        void show() const;
        const Stock& topval(const Stock& s) const;
        int numshares() const { return shares; }
        double shareval() const { return share_val; }
        double totalval() const { return total_val; }
        const string& co_name() const { return company; }
};
```

### 10.

`this` 指针可供类方法使用。它指向用于调用该方法的对象。因此，`this` 是对象的地址，而 `*this` 表示对象本身。

## 第11章复习题答案

### 1.

以下是类定义文件的原型和方法文件的函数定义：

```cpp
// prototype
Stonewt operator*(double mult);

// definition - let constructor do the work
Stonewt Stonewt::operator*(double mult)
{
    return Stonewt(mult * pounds);
}
```

### 2.

成员函数是类定义的一部分，由特定对象调用。成员函数可以隐式访问调用对象的成员，而不使用成员运算符。友元函数不是类的一部分，因此它作为普通函数调用来调用。它不能隐式访问类成员，因此必须对作为参数传递的对象使用成员运算符。例如，将复习题 1 的答案与复习题 4 的答案进行比较。

### 3.

要访问私有成员，它必须是友元；但要访问公有成员，它不必是友元。

### 4.

以下是类定义文件的原型和方法文件的函数定义：

```cpp
// prototype
friend Stonewt operator*(double mult, const Stonewt& s);

// definition - let constructor do the work
Stonewt operator*(double mult, const Stonewt& s)
{
    return Stonewt(mult * s.pounds);
}
```

### 5.

以下五个运算符不能重载：

```text
sizeof
.
.*
::
?:
```

### 6.

这些运算符必须通过使用成员函数来定义。
