
## 668 第14章 文件处理

新记录比原始记录多出六个字符。因此，字符超出 "h" 在 "worthington 将覆盖 0.00 以及文件中下一个顺序记录的开头。它是，格式化输入/输出模型使用流插入运算符 `<<` 和流提取运算符 `>>` 字段——因此记录——大小可能不同。例如，值 7、14–117、2074 和 27383 都是，存储相同数量的“原始数据”字节（通常在 32 位机器上为四个字节，在 64 位机器上可能为八个字节）。然而，当输出为格式化文本（字符序列）时，这些整数可以是不同大小的文件，具体取决于其实际值。格式化输入/输出模型通常不用于就地更新记录。第 14.7–14.11 节展示了如何使用固定长度记录进行就地更新。

这种更新可以很精细，但很笨拙。例如，要进行名称更改，可以将 300 while 0.00 之前的记录复制到新文件中，然后将更新后的记录写入新文件，并将 300 while 0.00 之后的记录复制到新文件。旧文件可以被删除，新文件重命名。这需要更新一条记录时处理文件中的每条记录。如果一次更新许多记录，尽管这种技术可以是可以接受的。

## 14.7 随机访问文件

到目前为止，我们已经看到如何创建顺序文件并搜索它们以定位信息。顺序文件不适合即时访问应用程序，其中特定记录必须立即加载。常见的即时访问应用程序是预订系统、银行系统、销售点系统、自动取款机和其他需要快速访问特定数据的交易处理系统。银行可能有数十万（或数百万）客户，然而，当客户使用自动取款机时，程序会立即检查该客户的账户是否资金充足。这种即时访问是通过随机访问文件实现的。随机访问文件的单个记录可以直接（并且快速）访问，而无需搜索其他记录。

正如我们所说，`C++` 不对文件施加结构。因此，应用程序必须创建要使用随机访问文件的文件。可以使用多种技术。也许最简单的方法是确保文件中所有记录的长度相同。相同大小的固定长度记录使程序能够快速计算（作为记录大小和记录键的函数）相对于文件开头的任何记录的确切位置。我们将看到这如何促进对特定记录的即时访问，即使在大量文件中也是如此。

图 14.7 说明了 `C++` 对由固定长度记录组成的随机访问文件的视图（每条记录在这种情况下为 100 字节长）。

数据可以插入到随机访问文件中，而不会破坏文件中的其他数据。之前存储的数据也可以在不重写整个文件的情况下进行更新或删除。在接下来的几节中，我们将解释如何创建随机访问文件、向文件中输入数据、顺序和随机读取数据、更新数据以及删除不再需要的数据。

## 14.8 创建随机访问文件

![](img/06ca63376760c659af4aa0e9c282068d_669_0.png)

图 14.7 随机访问文件的 C++ 视图。

`ostream` 成员函数 `write` 将指定数量的固定字节写入内存中的特定位置开始。当流与文件关联时，函数会在由 put 文件位置指针指示的文件位置写入数据。`istream` 成员函数 `read` 从指定流读取固定数量的字节到从指定地址开始的区域。如果流与文件关联，函数会从由“get”文件位置指针指示的文件位置读取字节。

### 14.8.1 使用 ostream 成员函数写入整数

使用语句将数字写入文件

```
outFile << number;
```

对于一个四字节整数可能占用 1 到 11 个字节——对于范围在 -2,147,483,647 到 2,147,483,647 之间的数字最多为 10 位数字，加上负数的符号。相反，我们可以使用语句

```
outFile.write(
    reinterpret_cast<const char*>(&number), sizeof(number));
```

它以表示整数数字的二进制字节形式写入。函数 `write` 将其第一个参数作为一组字节写入，通过将内存中的对象视为 `char*`，即指向字节的指针（请回忆 `char` 是一个字节）。从该位置开始，函数写入其第二个参数指定的字节数——一个类型为 `size_t` 的整数。如我们所见，`istream` 函数可用于将这四个字节读回整数变量 `number`。

### 14.8.2 使用 reinterpret_cast 运算符转换指针类型

不幸的是，传递给函数 `write` 作为第一个参数的指针并不是 `const char*`。为了输出其他类型的对象，我们必须将指向这些对象的指针转换为 `const char*`；否则，编译器将无法编译到函数 `write`。`C++` 提供了 `reinterpret_cast` 运算符用于此类情况，以明确表示你将数据视为不相关的类型。如果没有 `reinterpret_cast`，输出整数 `number` 的 `write` 语句将无法编译，因为编译器

不允许将 `int*` 类型的指针（由表达式 `&number` 返回的类型）传递给期望 `char*` 类型参数的函数——就编译器而言，这些类型不一致（即不兼容）。

`reinterpret_cast` 在编译时执行，并且不会更改其操作数所操作对象的数值。它要求编译器将操作数重新解释为目标类型（在关键字 `reinterpret_cast` 之后的角度括号中指定）。在图 14.10 中，我们使用 `reinterpret_cast` 将 `ClientData` 对象转换为其字节，以便输出到文件。随机访问文件处理程序很少写入单个字段到文件。通常，我们一次处理一个类的一个对象，如以下示例所示。

## 错误预防提示 14.3

不幸的是，很容易使用 `reinterpret_cast` 执行危险的操作，这可能导致严重的执行时错误。

## 可移植性提示 14.1

`reinterpret_cast` 取决于编译器，可能导致程序在不同平台上表现不同。仅在绝对必要时才使用此运算符。

## 可移植性提示 14.2

写入未格式化数据（由 `write` 写入）的程序必须在与写入数据的程序兼容的系统上编译和执行，因为不同系统可能以不同的方式表示内部数据。

### 14.8.3 信用处理程序

考虑以下问题陈述：

> 使用随机访问文件处理技术，创建一个信用处理程序，能够为最多可拥有 100 位客户的公司存储最多 100 条固定长度记录。每条记录应由具有键的账号、姓氏、名字和余额组成。程序应能够更新账户、插入新账户、删除账户并将所有账户记录插入到格式化文件以便打印。

下一节描述此信用处理程序。图 14.10 说明了打开随机访问文件、使用 `ClientData` 类的对象（图 14.8–14.9）定义记录格式并以二进制格式将数据写入磁盘。此程序使用函数 `write` 初始化文件 `credit` 的全部 100 条记录为空对象。每个对象包含账号 0、空的姓氏和名字字符串以及余额。

```
// Fig. 14.8: ClientData.h
// ClientData definition used in Fig. 14.10–14.13.
#ifndef CLIENTDATA_H
#define CLIENTDATA_H
#include <string>
```

图 14.8 | 用于图 14.10–14.13 的 `ClientData` 定义（第 1 部分，共 2 部分）

```
class ClientData {
public:
    // default ClientData constructor
    ClientData(int = 0, const std::string& = "",
        const std::string& = "", double = 0.0);
    // accessor functions for accountNumber
    void setAccountNumber(int);
    int getAccountNumber() const;
    // accessor functions for lastName
    void setLastName(const std::string&);
    std::string getLastName() const;
    // accessor functions for firstName
    void setFirstName(const std::string&);
    std::string getFirstName() const;
    // accessor functions for balance
    void setBalance(double);
    double getBalance() const;
private:
    int accountNumber;
    char lastName[15];
    char firstName[10];
    double balance;
};
#endif
```

图 14.8 | 用于图 14.10–图 14.13 的 `ClientData` 定义。（第 2 部分，共 2 部分。）

```
// ClientData.cpp
#include <string>
#include "ClientData.h"
using namespace std;
// default ClientData constructor
ClientData::ClientData(int accountNumberValue, const string& lastName,
    const string& firstName, double balanceValue)
    : accountNumber(accountNumberValue), balance(balanceValue) {
    setLastName(lastName);
    setFirstName(firstName);
}
// get-account-number value
int ClientData::getAccountNumber() const {return accountNumber;}
```

图 14.9 | `ClientData` 类存储客户的信用信息。（第 1 部分，共 2 部分。）

```
// set-account-number value
void ClientData::setAccountNumber(int accountNumber)
{
    accountNumber = accountNumber; // should validate
}
// get-last-name
string ClientData::getLastName() const { return lastName; }
// set-last-name
void ClientData::setLastName(const string& lastName) {
// copy at most 15 characters from string to lastName
size_t length = lastName.size();
length = (length < 15) ? length : 14;
lastName.copy(lastName, length);
lastName[length] = '\0'; // append null character to lastName
}
// get-first-name
string ClientData::getFirstName() const { return firstName; }
// set-first-name
void ClientData::setFirstName(const string& firstName) {
// copy at most 10 characters from string to firstName
size_t length = firstName.size();
length = (length < 10) ? length : 9;
firstName.copy(firstName, length);
firstName[length] = '\0'; // append null character to firstName
}
// get-balance-value
double ClientData::getBalance() const { return balance; }
// set-balance-value
void ClientData::setBalance(double balanceValue) { balance = balanceValue; }
```

图 14.9 | `ClientData` 类存储客户的信用信息。（第 2 部分，共 2 部分。）

`string` 类的对象没有统一的大小，而是动态分配内存以适应各种长度的字符串。我们必须维护固定长度的记录，因此 `ClientData` 类将客户的姓和名存储在固定长度的数组中（在 14.8 的第 31–32 行声明）。成员函数 `setLastName`（图 14.9，第 27–33 行）和 `setFirstName`（图 14.9，第 39–45 行）将字符串的每个字符复制到相应的 `char` 数组中。考虑函数 `setLastName`。第 29 行调用成员函数 `size` 以获取 `lastNameString` 的长度。第 30 行确保长度少于 15 个字符，然后第 31 行使用字符串成员函数 `copy` 将字符从 `lastNameString` 复制到 `char` 数组。第 32 行在 `char` 数组中插入空字符以终止 `lastName` 中的基于指针的字符串。成员函数 `setFirstName` 对名字执行相同的步骤。

## 14.9 随机读写数据到随机访问文件

### 14.8.4 以二进制模式打开文件用于输出

在 14.10 中，第 10 行为文件 `credit.dat` 创建了一个 `ofstream` 对象。构造函数中的第二个参数——`ios::out | ios::binary`——表示我们以二进制模式打开文件用于输出，如果要写入定长记录则需要此模式。多个文件打开模式通过使用 `|` 运算符将每个打开模式与下一个分隔开来管理，该运算符称为按位或运算符（第 22 章详细讨论了此运算符）。第 22-23 行导致 `blankClient`（在第 18 行使用默认参数构造）被写入与 `ofstream` 对象 `Credit` 关联的 `credit.dat` 文件中。`write` 的第一个参数必须是 `const char*` 类型。然而，`&blankClient` 的数据类型是 `ClientData*`。为了将 `&blankClient` 转换为 `const char*`，第 23 行使用了 `reinterpret_cast` 运算符，因此调用 `write` 时不会发出编译错误。

```
// Fig. 14.10 | Fig14_10.cpp
// Creating a randomly accessed file.
#include <iostream>
#include <fstream>
#include <cstdlib>
#include "ClientData.h" // ClientData class definition
using namespace std;

int main() {
    ofstream outCredit("credit.dat", ios::out | ios::binary);

    // exit program if ofstream could not open file
    if (!outCredit) {
        cerr << "File could not be opened." << endl;
        exit(EXIT_FAILURE);
    }

    ClientData blankClient; // constructor zeros out each data member

    // output 100 blank records to file
    for (int i=0; i < 100; ++i) {
        outCredit.write(reinterpret_cast<const char*>(&blankClient), sizeof(ClientData));
    }
}
```

Fig. 14.10 | Creating a random-access file with 100 blank records sequentially.

Figure 14.11 writes data to the file `credit.dat` and uses the combination of `fstream` functions `seekp` and `write` to store data at exact locations in the file. Function `seekp` sets the put pointer to a specific position in the file, then function `write` outputs the data. Line 6 includes the header `ClientData.h` defined in Fig.14.8, so the program can use `ClientData` objects.

## Chapter 14 File Processing
