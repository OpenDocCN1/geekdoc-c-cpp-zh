
## 14.3 创建顺序文件

C++ 不对文件施加任何结构。因此，像记录（[第1.4节](#)）这样的概念在 C++ 中并不存在。必须根据应用程序的要求来组织文件结构。下面的示例展示如何对文件施加简单的记录结构。

[图14.2](#) 创建了一个顺序文件，该文件可用于应收账款系统，帮助管理赊购客户欠公司的款项。对于每个客户，程序获取客户的账号、姓名和余额（即客户过去收到的商品和服务而欠公司的金额）。为每个客户获取的数据构成该客户的一条*记录*。账号充当*记录键*；也就是说，程序按账号顺序创建并维护文件中的记录。该程序假定用户按账号顺序输入记录。在完整的应收账款系统中，将提供*排序*功能，使用户能够*按任意顺序*输入记录——随后记录将被排序并写入文件。

```cpp
// Fig. 14.2: Fig14_02.cpp
// Creating a sequential file.
#include <iostream>
#include <string>
#include <fstream>  // contains file stream processing types
#include <cstdlib>  // exit function prototype
using namespace std;

int main() {
   // ofstream constructor opens file
   ofstream outClientFile( "clients.txt", ios::out );

   // exit program if unable to create file
   if ( !outClientFile ) {  // overloaded operator
      cerr << "File could not be opened" << endl;
      exit(EXIT_FAILURE);
   }

   cout << "Enter the account, name, and balance.\n"
        << "Enter end-of-file to end input.\n? ";

   int account;       // the account number
   string name;       // the account owner's name
   double balance;    // the account balance

   // read account, name and balance from cin, then place in file
   while ( cin >> account >> name >> balance ) {
      outClientFile << account << " " << name << " " << balance << endl;
      cout << "? ";
   }
}
```

```text
Enter the account, name, and balance.
Enter end-of-file to end input.
? 100 Jones 24.98
? 200 Doe 345.67
? 300 White 0.00
? 400 Stone -42.16
? 500 Rich 224.62
? ^Z
```

**图14.2 创建顺序文件。**

### 14.3.1 打开文件

图14.2 将数据写入文件，因此我们通过创建 `ofstream` 对象来打开文件以供输出。向该对象的构造函数（第11行）传递两个参数——**文件名**和**文件打开模式**。对于 `ofstream` 对象，文件打开模式可以是 `ios::out`（默认），用于将数据*输出*到文件；也可以是 `ios::app`，用于将数据*追加*到文件末尾（不修改文件中已有的任何数据）。第11行创建一个名为 `outClientFile` 的 `ofstream` 对象，并与为输出而打开的 `clients.txt` 文件关联——由于我们没有指定文件的路径（即其位置），该文件将位于程序所在的目录中。`ofstream` 构造函数打开文件——这会建立与文件的“通信线路”。在 C++11 之前，文件名被指定为基于指针的字符串——从 C++11 起，它也可以指定为 `string` 对象。

由于 `ios::out` 是默认值，第11行中的第二个构造函数参数不是必需的，因此我们本可以使用以下语句

```cpp
ofstream outClientFile("clients.txt");
```

以 `ios::out` 模式打开的现有文件会被**截断**——文件中的所有数据都会被*丢弃*。如果指定的文件尚**不**存在，则 `ofstream` 对象将使用该文件名*创建*文件。图14.3 列出了文件打开模式。这些模式也可以组合使用，如**第14.9节**所讨论。

![](img/ea0ad48f0d708c37231c1ca852bf6cf9_1772_0.png)

**错误预防提示14.1**

*在打开现有文件进行输出（`ios::out`）时要谨慎，尤其是当你希望保留文件内容时，因为这些内容会在没有任何警告的情况下被丢弃。*

**图14.3 文件打开模式。**

| 模式 | 描述 |
|---|---|
| `ios::app` | 将所有输出追加到文件末尾。 |
| `ios::ate` | 打开文件以供输出并移动到文件末尾（通常用于向文件追加数据）。数据可以写入文件中的*任意位置*。 |
| `ios::in` | 打开文件以供*输入*。 |
| `ios::out` | 打开文件以供*输出*。 |
| `ios::trunc` | *丢弃*文件内容（这也是 `ios::out` 的默认操作）。 |
| `ios::binary` | 以二进制（即*非文本*）方式打开文件以供输入或输出。 |

### 14.3.2 通过 `open` 成员函数打开文件

你可以创建一个 `ofstream` 对象而*不*打开特定文件——在这种情况下，文件可以在以后附加到该对象。例如，以下语句

```cpp
    ofstream outClientFile;
```

创建一个尚未与文件关联的 `ofstream` 对象。`ofstream` 成员函数 **open** 打开文件，并将其附加到*现有*的 `ofstream` 对象，如下所示：

```cpp
    outClientFile.open("clients.txt", ios::out);
```

同样，`ios::out` 是第二个参数的默认值。

### 14.3.3 测试文件是否成功打开

创建 `ofstream` 对象并*尝试*打开它之后，第14–17行（**图14.2**）中的 `if` 语句使用重载的 `ios` 成员函数 `operator!`（在**第13章**中讨论）来确定 `open` 操作是否成功。回想一下，如果流设置了 `failbit` 或 `badbit`，则 `operator!` 返回 `true`——在本例中，由于 `open` 操作失败，会设置其中一个或两个。一些可能的原因包括：

- 尝试打开一个*不存在的*文件进行读取
- 尝试从你没有访问权限的目录中打开文件进行读取或写入，以及
- 在没有可用磁盘空间时打开文件进行写入。

如果条件表明打开文件的尝试不成功，第15行会输出一条错误消息，第16行调用函数 `exit` 来终止程序。传给 `exit` 的参数会返回给调用该程序的环境。向 `exit` 传递 `EXIT_SUCCESS`（定义于 `<cstdlib>`）表示程序*正常*终止；传递任何其他值（本例中为 `EXIT_FAILURE`）表示程序因*错误*而终止。

### 14.3.4 重载的 `bool` 运算符

正如我们在**第13章**中讨论的，流的重载 `operator bool`（C++11 中新增）会将流转换为 `true` 或 `false` 值，因此可以在条件中测试它。如果流设置了 `failbit` 或 `badbit`，则重载运算符返回 `false`。`while` 语句（第27–30行）中的条件会*隐式地*在 `cin` 上调用 `operator bool` 成员函数。只要 `cin` 既未设置 `failbit` 也未设置 `badbit`，该条件就保持为 *true*。输入*文件结束*指示符会为 `cin` 设置 `failbit`。回想**第13章**中的内容，你也可以在输入对象上调用成员函数 `eof`。

### 14.3.5 处理数据

如果第11行成功打开文件，程序就开始处理数据。第19–20行提示用户输入每条记录的各字段，或者在数据输入完成时输入文件结束指示符。**图14.4** 列出了各种计算机系统输入文件结束的键盘组合。

**图14.4 文件结束键组合。**

| 计算机系统 | 键盘组合 |
|---|---|
| UNIX/Linux/Mac OS X | `<Ctrl-d>`（单独一行） |
| Microsoft Windows | `<Ctrl-z>`（然后按 *Enter*） |

第27行提取每组数据，并判断是否已输入文件结束。当遇到文件结束或输入了错误数据时，`operator bool` 返回 `false`，`while` 语句终止。用户输入文件结束，以通知程序不再处理其他数据。当用户输入文件结束键组合时，文件结束指示符会被设置。`while` 语句会循环，直到文件结束指示符被设置（或输入了错误数据）。

第28行使用流插入运算符 `<<` 和程序开始时与文件关联的 `outClientFile` 对象，将一组数据写入文件 `clients.txt`。这些数据可由专门读取该文件的程序检索（见第14.4节）。图14.2 创建的文件只是一个文本文件，因此可以用任何文本编辑器查看。

### 14.3.6 关闭文件

一旦用户输入文件结束指示符，`main` 就会终止。这会隐式调用 `outClientFile` 的析构函数，从而*关闭* `clients.txt` 文件。你也可以使用成员函数 `close` *显式地*关闭 `ofstream` 对象，如下所示：

```cpp
outClientFile.close();
```
