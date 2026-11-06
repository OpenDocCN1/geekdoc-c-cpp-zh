

### getline 函数从用户接收一行文本

有时候函数*并非*类的成员。这样的函数叫做**全局函数**。第18行

```cpp
getline(cin, theName); // read a line of text
```

使用 C++ 标准库全局函数 **getline** 从用户读取名称并将其放入变量 `theName` 中。与类 `string` 一样，函数 `getline` 需要 `<string>` 头文件，并且属于命名空间 `std`。

考虑为什么我们不能简单地写

```cpp
cin >> theName;
```

来获取账户名称。在我们的示例程序执行中，我们输入了名称“`Jane Green`”，它包含多个*由空格分隔*的单词。（回想在示例程序执行中我们用粗体突出显示用户输入。）读取 `string` 时，`cin` 在第一个*空白字符*（如空格、制表符或换行符）处停止。

因此，前面的语句只会读取 `"Jane"`。`"Jane"` 之后的信息*不会丢失*——它可以在程序后面由后续输入语句读取。

在这个例子中，我们希望用户输入完整名称（包括空格）并按 *Enter* 提交给程序。然后，我们希望将*整个*名称存储在 `string` 变量 `theName` 中。输入数据后按 *Enter*（或 *Return*）键时，系统会在输入流中插入一个换行符。函数 `getline` 从标准输入流对象 `cin` 读取用户输入的字符，直到换行符为止，但*不包括*该换行符，换行符会被*丢弃*；`getline` 将这些字符放入 `string` 变量 `theName` 中。

### 3.2.5 调用类 `Account` 的 `setName` 成员函数

`Account` 类的 `setName` 成员函数将账户名称存储到特定的 `Account` 对象中。第19行

```cpp
myAccount.setName(theName); // put theName in myAccount
```

调用 `myAccount` 的 `setName` 成员函数。成员函数调用可以提供**实参**来帮助函数执行其任务。将实参放在函数调用的括号中。这里，`theName` 的值（由第18行输入）是传递给 `setName` 的*实参*，`setName` 将该值存入对象 `myAccount` 中。

从 `main` 的角度看，当调用 `setName` 时：

1. 程序将执行流程从 `main` 中的第19行转移到 `setName` 成员函数的定义。调用将调用括号中的*实参*值——即 `theName` 对象的值——传递给该函数。因为 `setName` 是通过 `myAccount` 对象调用的，所以 `setName` “知道”要操作的具体对象。
2. 接下来，成员函数 `setName` 将实参的值存入 `myAccount` 对象。
3. 当 `setName` 执行完毕时，程序执行流程返回到调用 `setName` 的地方（第19行），然后继续执行到第22行。

### 显示用户输入的姓名

为了证明 `myAccount` 现在包含用户输入的姓名，第22–23行

```cpp
cout << "Name in object myAccount is: "
     << myAccount.getName() << endl;
```

再次调用成员函数 `getName`。如程序输出的最后一行所示，第18行中用户输入的姓名被显示出来。当该语句执行完毕时，到达 `main` 的末尾，程序终止。

## 3.3 具有数据成员以及 set 和 get 成员函数的 `Account` 类

我们已经看到了 `Account` 类的实际应用（**图3.1**），现在展示 `Account` 类的细节。然后，我们给出一个 UML 图，以简洁的图形表示形式概括 `Account` 类的*属性*和*操作*。

### 3.3.1 Account 类定义

类 `Account`（图3.2）包含一个 `name` **数据成员**，用于存储账户持有人的姓名。类的数据成员维护该类每个对象的数据。在本章后面，我们将添加 `balance` 数据成员以跟踪每个 `Account` 中的金额。类 `Account` 还包含成员函数 `setName`，程序可以调用该函数在 `Account` 对象中存储姓名，以及成员函数 `getName`，程序可以调用该函数从 `Account` 对象中获取姓名。

```cpp
// Fig. 3.2: Account.h
// Account class that contains a name data member
// and member functions to set and get its value.
#include <string> // enable program to use C++ string data type

class Account {
public:
    // member function that sets the account name in the object
    void setName(std::string accountName) {
        name = accountName; // store the account name
    }

    // member function that retrieves the account name from the object
    std::string getName() const {
        return name; // return name's value to this function's caller
    }
private:
    std::string name; // data member containing account holder's name
}; // end class Account
```

**图3.2** 包含 `name` 数据成员以及设置和获取其值的成员函数的 `Account` 类。

### 3.3.2 关键字 `class` 和类体

*类*定义从第6行开始：

```
class Account {
```

每个类定义都包含关键字 **class**，其后紧跟类名——本例中是 `Account`。每个类体都括在左花括号（第6行末尾）和右花括号（第19行）中。类定义以*必需的*分号（第19行）结束。为了可重用性，请将每个类定义放在单独的扩展名为 `.h` 的头文件中（本例为 `Account.h`）。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_302_0.png)

### *常见编程错误 3.1*

*在类定义末尾忘记分号是一个语法错误。*

### *标识符和驼峰命名*

类名、成员函数名和数据成员名都是*标识符*。按照惯例，变量名标识符以小写字母开头，名称中第一个单词之后的每个单词都以大写字母开头——例如，`firstNumber` 的第二个单词 `Number` 以大写 `N` 开头。这种命名约定称为**驼峰命名**，因为大写字母像骆驼的驼峰一样突出。同样按照惯例，类名以大写字母开头，成员函数名和数据成员名以小写字母开头。

### 3.3.3 `string` 类型的数据成员 `name`

回想第1.8节，对象具有属性，这些属性以数据成员的形式实现。对象在其整个生命周期中都携带这些属性。每个对象都有自己的一份类数据成员的副本。通常，一个类还包含一个或多个成员函数。这些成员函数操作属于该类的特定对象的数据成员。数据成员存在于：

- *在*程序对对象调用成员函数*之前*，
- *在*成员函数执行*期间*，以及
- *在*成员函数执行完成*之后*。

数据成员声明在*类定义内部*但*成员函数体外部*。第18行

```cpp
std::string name; // data member containing account holder’s name
```

声明了类型为 `string` 的数据成员 `name`。如果有很多 `Account` 对象，每个对象都有自己的 `name`。由于 `name` 是一个数据成员，它可以被类的每个成员函数操作。`string` 的默认值是**空字符串**（即 `""`）——这就是为什么 `main` 中的第13行（[图3.1]）第一次调用 `myAccount` 的 `getName` 成员函数时没有显示姓名。[第3.4节] 解释了 `string` 如何获得其默认值。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_305_0.png)

### *良好编程实践 3.1*

*按照惯例，将类的数据成员放在类体的最后。你可以在类的成员函数定义之外的任何位置列出类的数据成员，但分散数据成员会导致代码难以阅读。*

### *在头文件中将 `std::` 用于标准库组件*

在整个 `Account.h` 头文件（[图3.2]）中，我们引用 `string` 时使用 `std::`（第9、14和18行）。出于我们将在第23.4节中解释的微妙原因，头文件*不应*包含 `using` 指令或 `using` 声明。

