

```cpp
// process user's request
while (request != RequestType::END) {
    switch (request) {
        case RequestType::ZERO_BALANCE:
            cout << "\nAccounts with zero balances:\n";
            break;
        case RequestType::CREDIT_BALANCE:
            cout << "\nAccounts with credit balances:\n";
            break;
        case RequestType::DEBIT_BALANCE:
            cout << "\nAccounts with debit balances:\n";
            break;
    }
}

int account; // the account number
string name; // the account owner's name
double balance; // the account balance

// read account, name and balance from file
inClientFile >> account >> name >> balance;

// display file contents (until eof)
while (!inClientFile.eof()) {
    // display record
    if (shouldDisplay(request, balance)) {
        outputLine(account, name, balance);
    }
}

// read account, name and balance from file
inClientFile >> account >> name >> balance;
inClientFile.clear(); // reset eof for next input
inClientFile.seekg(0); // reposition to beginning of file
request = getRequest(); // get additional request from user
}

cout << "End of run." << endl;
}

// obtain request from user
RequestType getRequest() {
   // display request options
   cout << "\nEnter request\n"
      << " 1 - List accounts with zero balances\n"
      << " 2 - List accounts with credit balances\n"
      << " 3 - List accounts with debit balances\n"
      << " 4 - End of run." << fixed << showpoint;
   int type; // request from user

   do { // input user request
      cout << "\n? ";
      cin >> type;
   } while (type < static_cast<int>(RequestType::ZERO_BALANCE) ||
            type > static_cast<int>(RequestType::END));

   return static_cast<RequestType>(type);
}

// determine whether to display given record
bool shouldDisplay(RequestType type, double balance) {
   // determine whether to display zero balances
   if (type == RequestType::ZERO_BALANCE && balance == 0) {
      return true;
   }

   // determine whether to display credit balances
   if (type == RequestType::CREDIT_BALANCE && balance < 0) {
      return true;
   }

   // determine whether to display debit balances
   if (type == RequestType::DEBIT_BALANCE && balance > 0) {
      return true;
   }

   return false;
}

// display single record from file
void outputLine(int account, const string& name, double balance) {
   cout << left << setw(10) << account << setw(13) << name
      << setw(7) << setprecision(2) << right << balance << endl;
}
```

```text
Enter request
  1 - List accounts with zero balances
  2 - List accounts with credit balances
  3 - List accounts with debit balances
  4 - End of run
? 1

Accounts with zero balances:
300      White          0.00

Enter request
  1 - List accounts with zero balances
  2 - List accounts with credit balances
  3 - List accounts with debit balances
  4 - End of run
? 2

Accounts with credit balances:
400      Stone         -42.16

Enter request
  1 - List accounts with zero balances
  2 - List accounts with credit balances
  3 - List accounts with debit balances
  4 - End of run
? 3

Accounts with debit balances:
100      Jones          24.98
200      Doe           345.67
500      Rich          224.62

Enter request
  1 - List accounts with zero balances
  2 - List accounts with credit balances
  3 - List accounts with debit balances
  4 - End of run
? 4
End of run.
```

图 14.6 信用查询程序。

## 14.5 C++14：读写带引号的文本

许多文本文件包含带引号的文本，例如 `"C++ How to Program"`。例如，在表示 HTML5 网页的文件中，属性值用引号括起来。如果你正在构建一个 Web 浏览器来显示此类网页的内容，就必须能够读取这些带引号的字符串并去掉引号。

假设你需要从文本文件中读取数据，就像在 **图 14.5** 中所做的那样，但每个账户的数据格式如下：

```text
100 "Janie Jones" 24.98
```

回想一下，流提取运算符 `>>` 将空白字符视为分隔符。因此，如果我们使用 **图 14.5** 第 30 行中的表达式读取前面的数据

```cpp
inClientFile >> account >> name >> balance;
```

第一次流提取将 `100` 读入 `int` 变量 `account`，第二次只将 `"Janie` 读入 `string` 变量 `name`（开头的双引号会成为 `name` 中 `string` 的一部分）。第三次流提取在尝试为 `double` 变量 `balance` 读取值时失败，因为输入流中的下一个标记（即数据片段）——`Jones"`——不是 `double`。

### 读取带引号的文本

C++14 新增的流操纵符——`quoted`（头文件 `<iomanip>`）——使程序能够从流中读取带引号的文本，*包括*带引号文本中的任何空白字符，并丢弃双引号分隔符。例如，如果我们使用以下表达式读取前面的数据

```cpp
inClientFile >> account >> quoted(name) >> balance
```

第一次流提取将 `100` 读入 `account`，第二次将 `Janie Jones` 作为一个 `string` 读取，并在不带双引号分隔符的情况下存储到 `name` 中，第三次流提取将 `24.98` 读入 `balance`。如果带引号的数据包含 `\"` 转义序列，则每个转义序列都会被读取，并作为转义序列 `\"` 存储在 `string` 中——而不是作为 `"`。

### 写出带引号的文本

类似地，你可以将带引号的文本写入流。例如，如果 `name` 包含 `Janie Jones`，则语句

```cpp
outputStream << quoted(name);
```

会向基于文本的 `outputStream` 写入

```text
"Janie Jones"
```

## 14.6 更新顺序文件

如 **14.3 节** 所示，格式化并写入顺序文件的数据在修改时可能破坏文件中的其他数据。例如，如果需要将名称“`White`”改为“`Worthington`”，则覆盖旧名称会损坏文件。`White` 的记录写入文件时如下

```text
300 White 0.00
```

如果使用更长的名称从文件中的同一位置重写这条记录，那么记录会变成

```text
300 Worthington 0.00
```

新记录比原记录多六个字符。因此，“`Worthington`”中“h”之后的字符将覆盖 `0.00` 以及文件中下一条顺序记录的开头。问题在于，在使用流插入运算符 `<<` 和流提取运算符 >> 的格式化输入/输出模型中，字段——因而记录——的大小可以变化。例如，值 7、14、−117、2074 和 27383 都是 `int`，它们在内部存储相同数量的“原始数据”字节（在 32 位机器上通常为四个字节，在某些 64 位机器上可能为八个字节）。然而，当作为格式化文本（字符序列）输出时，这些整数会根据其实际值变成不同大小的字段。因此，格式化输入/输出模型通常不用于*就地*更新记录。**14.7～14.11 节** 展示了如何使用固定长度记录执行就地更新。

这种更新可以完成，但很笨拙。例如，要进行前面的名称更改，可以将顺序文件中 `300 White 0.00` 之前的记录*复制*到新文件，然后将更新后的记录写入新文件，再将 `300 White 0.00` 之后的记录复制到新文件。之后可以删除旧文件并重命名新文件。这需要处理文件中的*每*一条记录才能更新一条记录。不过，如果一次遍历文件就要更新许多记录，这种技术是可以接受的。

## 14.7 随机存取文件

到目前为止，我们已经了解了如何创建顺序文件并搜索它们以定位信息。顺序文件不适合**即时访问应用**，在这类应用中，必须立即定位特定记录。常见的即时访问应用包括飞机订票系统、银行系统、销售点系统、自动取款机以及其他需要快速访问特定数据的**事务处理系统**。一家银行可能有数十万（甚至数百万）其他客户，然而，当客户使用自动取款机时，程序几乎立即检查该客户是否有足够资金。这种即时访问通过**随机存取文件**成为可能。随机存取文件中的各条记录可以直接（且快速地）访问，而不必搜索其他记录。

正如我们所说，C++ 不对文件施加结构。因此，想要使用随机存取文件的应用程序必须创建它们。可以使用多种技术。也许最简单的方法是要求文件中的所有记录都具有*相同的固定长度*。使用大小相同、长度固定的记录使程序可以轻松地快速计算（根据记录大小和记录键）任何记录相对于文件开头的准确位置。我们很快将看到，这如何促进对特定记录的*立即访问*，即使是在巨大的文件中。

