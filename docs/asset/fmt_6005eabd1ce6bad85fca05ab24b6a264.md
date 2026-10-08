
在这种情况下，字符串参数 `"Jane Green"` 被传递给 `Account` 类的构造函数，并用于初始化 `account1` 对象的 `name` 数据成员。前面的语句假设 `Account` 类有一个只接受一个字符串参数的构造函数。

- 8. 在第 9.6 节中，你将学习类可以有多个构造函数。

## 3.4 Account 类：使用构造函数初始化对象

### 3.4.1 定义自定义对象化的 Account 构造函数

图 3.4 显示了带有构造函数的 `Account`，该构造函数接收 `accountName` 参数并在创建 `Account` 对象时使用它来初始化数据成员 `name`。

```cpp
// Fig 3.4: Account.h
// 带有初始化账户名称的构造函数的 Account 类。
#include <string>
class Account {
public:
    explicit Account(std::string accountName)
        : name(accountName) // 成员初始化
        {} // 函数体为空
    // 设置账户名称的函数
    void setName(std::string accountName)
    // 获取账户名称的函数
    std::string getName() const
private:
    std::string name;
};
```

**图 3.4** | 带有初始化账户名称的构造函数的 Account 类。

**Account 构造函数**

图 3.4 显示了 `Account` 类，其构造函数接收 `accountName` 参数并在创建 `Account` 对象时使用它来初始化数据成员 `name`。

```cpp
explicit Account(std::string accountName)
    : name(accountName) // 成员初始化
    {} // 函数体为空
```

构造函数的定义在 3.4 的第 8-11 行。构造函数是 `explicit` 的，因为它接收一个参数——其重要的原因将在第 10.3 节中学习。现在将所有单参数构造函数声明为 `explicit`。

## explicit 关键字

我们将此构造函数声明为 `explicit`，因为它接收一个参数——其重要的原因将在第 10.3 节中学习。现在将所有单参数构造函数声明为 `explicit`。3.4 的第 8 行没有指定返回类型，因为构造函数不能返回值——即使是 `void` 也不行。此外构造函数不能声明为 `const`。

## 在构造函数和成员函数中使用相同参数

回顾第 3.3 节，函数参数是局部变量。在 3.4 中，构造函数和 `setName` 函数都有名为 `accountName` 的参数。尽管它们的标识符相同，第 8 行的参数是构造函数的局部变量，`setName` 不可见。同样，第 14 行的参数是 `setName` 的局部变量，构造函数可见。这种可见性被称为作用域，将在第 6.10 节中讨论。

### 3.4.2 在创建时初始化 Account 对象

`AccountTest` 程序 (3.5) 使用构造函数初始化两个不同的 `Account` 对象。第 11 行

```cpp
account1{"Jane Green"};
```

创建了 `Account` 对象。当你创建一个对象时，C++ 会隐式调用类的构造函数来初始化它。如果构造函数有参数，你在对象变量名右侧的大括号 `{}` 中放置相应的参数。在第 11 行中，参数 `"Jane Green"` 初始化了新对象的数据成员 `name`。

```cpp
account2{"John Blue"};
```

重复了此操作，传递参数 `"John Blue"` 来初始化 `account2` 的 `name`。第 15-16 行使用每个对象的 `setName` 成员函数获取名称，并证明它们在对象创建时已通过初始化。输出显示了不同的名称，证实了每个 `Account` 都维护自己的 `name` 数据成员副本。

> 性能提示 3.1
> 你可以在构造函数体中使用成员初始化列表进行初始化，你将在第 9 章中了解到某些类型的数据成员应该以这种方式初始化。

## 3.4 Account 类：使用构造函数初始化对象

```cpp
// Fig. 3.5: AccountTest.cpp
// 使用 Account 构造函数在每个 Account 对象
// 创建时初始化 name 数据 
// 成员。
#include <iostream>
#include "Account.h"
using namespace std;
int main() {
    // 创建两个 Account 对象
    Account account1{"Jane Green"};
    Account account2{"John Blue"};
    // 显示每个 Account 的 name 值
    cout << "account1 name: " << account1.getName() << endl;
    cout << "account2 name: " << account2.getName() << endl;
}
```

Fig. 3.5 | 在创建 Account 对象时，使用 Account 构造函数来初始化 name 数据成员。

### 默认构造函数
回想图 3.1 中的第 10 行

```cpp
Account myArray;
```

在没有在对象变量右侧放置大括号的情况下创建了一个 Account 对象。在这种情况下，C++ 会隐式地调用类的默认构造函数。在任何没有显式定义构造函数的类中，编译器都会提供一个无参数的默认构造函数。默认构造函数不会初始化类的基础数据类型成员，但它会调用每个作为另一个类对象的数据成员的默认构造函数。例如，在图 3.2 的 Account 类中，类的默认构造函数会调用 `string` 的构造函数来将数据成员初始化为空字符串。未初始化的基础类型变量包含未定义的（“垃圾”）值。10

### 在定义了构造函数的类中没有默认构造函数
如果你为类定义了自定义的构造函数，编译器将不会为该类创建默认构造函数。在这种情况下，你将无法像我们在图 3.1 中那样通过以下方式创建 Account 对象：

```cpp
Account myArray;
```

除非你定义的自定义构造函数具有一个空参数列表。我们稍后会看到，C++11 允许你即使定义了非默认构造函数，也能强制编译器创建默认构造函数。

10. 我们将在第 6.10 节看到关于此的例外情况。

## 软件工程观察 3.1
除非你的类数据成员的默认初始化是可以接受的，否则你通常应该提供一个自定义构造函数，以确保在创建类的每个新对象时，你的数据成员都能用有意义的值正确初始化。

## 3.4.3 带有构造函数的 Account UML 类图
图 3.6 的 UML 类图对图 3.4 中的 Account 类进行了建模，它有一个带有 `accountName` 参数的构造函数。与操作（图 3.3）一样，UML 在类图的第三部分建模构造函数。为了区分构造函数和类的操作，UML 要求将“constructor”一词括在双角号（« »）中并放在构造函数名称之前。惯例是在第三部分中将构造函数列在其他操作之前。

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_128_0.png)

Fig. 3.6 | 图 3.4 Account 类的 UML 类图。

## 3.5 使用 set 和 get 成员函数的软件工程
正如下一节中看到的，`set` 和 `get` 成员函数可以分别验证修改数据的控制尝试以及该数据呈现给调用者的方式。这些都是极具吸引力的软件工程益处。

如果数据成员是公共的，类的客户端——即任何可以调用类成员的其他代码——都可以看到它在做什么，并对它做任何事情，包括将其赋值为无效值。

你可能会认为，即使类无法访问私有数据成员，客户端仍然可以通过公有的 `set` 和 `get` 函数对变量做任何它想做的事。你会认为你可以随时通过公有的 `get` 函数查看私有数据（并确切地看到它如何在对象中存储的），并且可以通过公有的 `set` 函数修改数据。

实际上，`set` 可以被设计为验证其参数并拒绝任何将数据设置为坏值的尝试，例如：

- - 负温度的体温
- 3 月份中不在 1 到 31 范围内的日期
- 不在公司产品目录中的产品代码等。

而 `get` 函数可以以不同的形式呈现数据，而实际表示保持对用户隐藏。例如，`get` 函数可能会以不同的形式呈现数据，而实际表示保持隐藏。

## 3.6 带有余额的类：数据验证
控制对数据的访问可以减少错误，增加程序的健壮性和用性。变化是规则而非例外。你应该预见到你的代码可能会被修改，并且经常如此。

**软件工程观察 3.2**
使用公有的 `set` 和 `get` 函数来控制私有数据使程序更清晰、更易维护。

**软件工程观察 3.3**
紧密控制数据的呈现可以极大减少错误，增加安全性和用性。

### 带有封装数据的 Account 对象概念视图
你可以像图 3.7 所示将 Account 对象想为：其私有数据隐藏在对象内部，用户只能通过调用公有的 `set` 和 `get` 函数来与其进行交互。

![](img/d9ae0ed4c13d4f57e9ae2c92e9fdf0b7_128_0.png)

Fig. 3.7 | 封装数据的 Account 对象的视图。

**软件工程观察 3.4**
通常，数据成员应该是私有的，成员函数应该是公的。在第 2 章中我们使用 `int` 类型表示整数。为了简单起见，我们将使用 `int` 类型表示账户余额。

### 3.6.1 数据成员
典型的银行服务许多账户，每个账户都有自己的余额。在更新后的 Account 类中（图 3.8），第 42 行

声明了一个 `int` 类型的余额数据成员并将其初始化为 0。

```cpp
int balance(0); // 带有默认值的数据成员
```

这被称为类内初始化，并在 C++11 中引入。Account 对象包含了其名称和余额的自己的副本。

```cpp
// Fig. 3.8: Account.h
// 带有 name 和 balance 数据成员的 Account 类，其构造函数和 deposit 函数都进行验证。
#include <string>
class Account {
public:
    // 带有两个参数的 Account 构造函数
    Account(std::string accountName, int initialBalance)
    : name(accountName) { // 将 accountName 赋值给数据成员
    // 验证 initialBalance 是否大于 0；否则
    // 数据成员余额保持其默认初始值 0
    if (initialBalance > 0) { // 如果 initialBalance 有效
        balance = initialBalance; // 将其赋值给数据成员
    }
    // 只向余额存款有效金额的函数
    void deposit(int depositAmount) {
        if (depositAmount > 0) { // 如果 depositAmount 有效
            balance = balance + depositAmount; // 将加到余额
        }
    }
    // 返回账户余额的函数
    int getBalance() const {
        return balance;
    }
    // 设置名称的函数
    void setName(std::string accountName) {
        name = accountName;
    }
    // 返回名称的函数
    std::string getName() const {
        return name;
    }
private:
    std::string name; // 账户名称数据成员
    int balance(0); // 带有默认值的数据成员
}; // 类 Account 类
```

## 3.6 带有余额的账户类：数据验证

### 账户的成员函数都可以使用 balance
第 15、22 和 28 行的语句使用了 `balance` 变量，尽管它没有在任何成员函数中声明。我们可以在这些成员函数中使用 `balance`，因为它是同一个类定义中的数据成员。

### 3.6.2 带有验证的双参数构造函数

该类有一个构造函数和四个成员函数。人们在开立账户时立即存款是常见现象，因此构造函数（第 9–17 行）接收第二个参数——代表初始余额的类型 `initialBalance`。我们没有显式声明这个构造函数（如图 3.4 所示），因为这个构造函数有多个参数。

图 3 的第 14–16 行：

```cpp
if (initialBalance > 0) { // 如果 initialBalance 有效
    balance = initialBalance; // 分配给数据成员 balance
}
```

确保只有在值大于 0 时才将 `initialBalance` 的值分配给数据成员 `balance`——这就是验证或有效性检查的作用。否则，第 15 行会将 `initialBalance` 的值分配给数据成员。否则，`balance` 将保持为 0——它的默认值在 Account 定义的第 4 行设置。

### 3.6.3 带有验证的 deposit 成员函数

成员函数 `deposit`（第 20–24 行）在完成任务时不返回任何数据，因此其返回类型为 `void`。该成员函数接收一个名为 `depositAmount` 的参数。第 21–23 行：

```cpp
if (depositAmount > 0) { // 如果 depositAmount 有效
    balance = balance + depositAmount; // 加到余额
}
```

确保只有在参数有效（即大于零）时才将 `depositAmount` 的值加到余额中——这是有效性的另一个另一个例子。第 22 行首先将当前余额和 `depositAmount` 相加，形成一个临时和并赋值给 `balance`，替换其原有值（该加法的优先级高于赋值）。重要的是，理解第 22 行赋值运算符右侧的计算 `balance += depositAmount` 并不会修改 `balance`——这就是为什么赋值是必要的。第 4.12 节展示了第 22 行的简洁写法。

### 3.6.4 getBalance 成员函数

成员函数 `getBalance`（第 27–29 行）允许类的客户端获取特定 Account 对象的余额值。该成员函数指定了返回类型 `int` 和空参数列表。成员函数 `getName` 和 `getBalance` 被声明为 `const`，因为在返回返回过程中，它们没有、也不应该修改被调用的 Account 对象。

第 3 章 类、对象、成员函数和字符串简介

### 3.6.5 操作带有余额的账户对象

图 3.9 中的 `main` 函数创建了两个 Account 对象（第 10–11 行），并尝试用 50 的有效余额和 -7 的无效余额对它们进行初始化——为了示例示例，我们假设余额必须大于或等于 0。第 14–17 行输出账户名称和余额，这些值是通过调用 Account 的 `getName` 和 `getBalance` 函数获得的。

```cpp
// Fig 3.9: AccountTest.cpp
// 显示并更新余额。
#include <iostream>
#include "Account.h"
using namespace std;
int main() {
    Account account1("Jane Green", 50);
    Account account2("John Blue", -7);
    // 显示每个对象的余额
    cout << "account1: " << account1.getName() << " balance is $" << account1.getBalance();
    cout << "account2: " << account2.getName() << " balance is $" << account2.getBalance();
    cout << "\nenter deposit amount for account1: "; // 提示
    int depositAmount;
    cin >> depositAmount; // 获取输入
    cout << "adding " << depositAmount << " to account1 balance";
    account1.deposit(depositAmount);
    // 显示余额
    cout << "account1: " << account1.getName() << " balance is $" << account1.getBalance();
    cout << "account2: " << account2.getName() << " balance is $" << account2.getBalance();
    cout << "\ner deposit amount for account2: "; // 提示
    cin >> depositAmount; // 获取输入
    cout << "adding " << depositAmount << " to account2 balance";
}
```
