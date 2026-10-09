
```cpp
// Fig. 14.11: Fig14_11.cpp
// Writing to a random-access file.
#include <iostream>
#include <fstream>
#include <cstdlib>
#include "ClientData.h" // ClientData definition
using namespace std;

int main() {
    fstream outCredit("credit.dat", ios::in | ios::out | ios::binary);

    // exit program if fstream cannot open file
    if (!outCredit) {
        cerr << "File could not be opened." << endl;
        exit(EXIT_FAILURE);
    }

    cout << "Enter account number (1 to 100, 0 to end input)?";

    int accountNumber;
    string lastName;
    string firstName;
    double balance;

    cin >> accountNumber; // read account number
    // user enters information, which is copied into file
    while (accountNumber != 0 && accountNumber <= 100) {
        // user enters last name, firstName and balance
        cout << "Enter lastname, firstName and balance\n";
        cin >> lastName;
        cin >> firstName;
        cin >> balance;

        // create ClientData object
        ClientData client(accountNumber, lastName, firstName, balance);

        // seek position in file of user-specified record
        outCredit.seekp((client.getAccountNumber() - 1) * sizeof(ClientData));

        // write user-specified information in file
        outCredit.write(reinterpret_cast<const char*>(&client), sizeof(ClientData));

        // enable user to enter another account
        cout << "Enter account number\n";
        cin >> accountNumber;
    }
}
```

Fig. 14.11 | Writing to a random-access file. (Part 1 of 2).

### 14.10 顺序读取随机访问文件

```
Enter account number (1 to 100, 0 to end input)
? 37
Enter lastname, firstname balance
? Barker Doug 0.00
Enter account number
? 29
Enter lastname, firstname balance
? Brown Nancy -24.54
Enter account number
? 96
Enter lastname, firstname balance
? Stone Sam 34.98
Enter account number
? 88
Enter lastname, firstname balance
? Smith Dave 258.34
Enter account number
? 33
Enter lastname, firstname balance
? Dunn Stacey 314.33
Enter account number
? 0
```

Fig. 14.11 | Writing to a random-access file (Part 2 of 2)

### 14.9.1 以二进制模式打开文件用于输入和输出

第 10 行使用 `fstream` 对象 `outCredit` 打开现有的 `.dat` 文件。文件通过创建文件模式 `ios::in`、`ios::out` 和 `ios::binary` 以二进制模式打开用于输入和输出。请注意，因为我们使用了 `ios::in`，如果文件不存在，将会发生错误并且文件不会被打开。以这种方式打开现有的 `.dat` 文件可确保此程序可以操作由图 14.10 的程序写入文件的记录，而不是从头创建文件

### 14.9.2 定位文件位置指针

第 39-40 行将对象 `outCredit` 的文件位置指针定位到由以下计算的字节位置：

```
(client.getAccountNumber() - 1) * sizeof(ClientData)
```

因为账号在 1 到 100 之间，我们在计算记录的字节位置时减去 1。因此，对于记录 1，文件位置指针被设置为 0——文件的开头。对于记录 2，文件位置指针被设置为 1* `sizeof(ClientData)`，依此类推。

## 14.10 顺序读取随机访问文件

在前面的章节中，我们创建了一个随机访问文件并向该文件写入数据。在本节中，我们开发一个程序顺序读取文件并仅打印包含数据的记录。这些程序产生额外的好处。看看你能否确定它是什么；我们在本节末尾揭示它。

流函数 `read` 从流中当前位置输入指定数量的字节到对象中。例如，第 28 行（图 14.12）读取

`sizeof(ClientData)` by the file associated with `inCredit` and stores the data in

`client`. Function requires a first argument of type `char*`. Since `&client` is of type

`ClientData*`, `&client` must be cast to `char*` using the cast operator `reinterpret_cast`.

```cpp
// Fig. 14.12: Fig14_12.cpp
// Reading a random-access file sequentially.
#include <iostream>
#include <iomanip>
#include <fstream>
#include <cstdlib>
#include "ClientData.h" // ClientData class definition
using namespace std;

void outputLine(ostream&, const ClientData&); // prototype

int main() {
    ifstream inCredit("credit.dat", ios::in | ios::binary);

    // exit program if inCredit cannot open file
    if (!inCredit) {
        cerr << "File could not be opened." << endl;
        exit(EXIT_FAILURE);
    }

    // output column heads
    cout << left << setw(10) << "Account" << setw(16) << "Last Name"
         << setw(11) << "First Name" << setw(10) << right << "Balance\n";

    ClientData client; // create record
    // read first record from file
    inCredit.read(reinterpret_cast<char*>(&client), sizeof(ClientData));

    // read all records from file
    while (inCredit) {
        // display record
        if (client.getAccountNumber() != 0) {
            outputLine(cout, client);
        }
        // read next from file
        inCredit.read(reinterpret_cast<char*>(&client), sizeof(ClientData));
    }
}

// display record
void outputLine(ostream& output, const ClientData& record) {
    cout << left << setw(10) << record.getAccountNumber()
         << setw(16) << record.getLastName()
         << setw(11) << record.getFirstName()
         << setw(10) << setprecision(2) << right << fixed
         << showpoint << record.getBalance() << endl;
}
```

Fig. 14.12 | Reading a random-access file sequentially. (Part I of 2.)

## 14.11 案例研究：事务处理程序

| Account | Last Name | First Name | Balance |

|---|---|---|---|

| 29 | Brown | Nancy | -24.54 |

| 33 | Dunn | Stacey | 314.33 |

| 37 | Barker | Doug | 0.00 |

| 88 | Smith | Dave | 258.34 |

| 96 | Stone | Sam | 34.98 |

Fig. 14.12 Reading a random-access file sequentially. (Part 2 of 2)

14.12 读取 `credit.dat` 文件中的每条记录，检查每条记录是否包含数据，并格式化包含数据的记录的输出。第 31 行的条件限制流的 `operator bool` 以确定是否到达文件末尾或读取文件时是否发生错误——在这两种情况下 `while` 语句都会执行。从文件中输入的数据由函数 `output`（第 43-49 行）输出，该函数接收两个参数——`ofstream` 对象的引用和要输出的 `clientData` 结构。输出参数类型是插入，因为任何 `ofstream` 对象（如 `cout`）或 `stream` 的派生类对象（如 `ofstream` 对象）都可以作为参数提供。此相同的函数可用于将输出执行到标准输出流和文件流，而无需编写函数。

我们之前在本节开头承诺的额外好处是什么？如果你检查输出窗口，你会注意到记录按账号号排序列出。使用直接访问技术。排序使用直接访问技术相对较快。速度是通过使文件足够大以容纳可能创建的每条记录来实现的。当然，文件可能大部分时间都稀疏占用，导致存储浪费。这就是空间-时间权衡的例子；通过使用大量空间，我们可以开发出更快的排序算法。幸运的是，存储价格的持续下降使这个问题变得不那么重要。

## 14.11 案例研究：事务处理程序

我们现在介绍一个实质性的事务处理程序（图 14.13），使用随机访问文件实现即时访问处理。该程序维护银行的账户信息。它更新账户、添加删除并存储所有当前账户的格式化列表到文本文件中。我们假设图 14.10 的程序已执行以创建 `credit.dat`，并且图 14.11 的程序已执行以插入初始数据。第 25 行通过创建用于二进制格式的读写 `ofstream` 来打开 `credit.dat` 文件。

```cpp
// Fig 14.13: Fig14_3.cpp
// This program reads a random-access file sequentially, updates
// data previously written to the file, creates data to be placed
// in the file, and deletes data previously stored in the file.
```

Fig. 14.13 Bank-account program. (Part I of 6.)

## 678 第14章 文件处理

```cpp
#include <iostream>
#include <fstream>
#include <iomanip>
#include <cstdlib>
#include "ClientData.h" // ClientData class definition
using namespace std;

enum class Choice { PRINT = 1, UPDATE, NEW, DELETE, END };

Choice enterChoice();
void createTextFile(fstream&);
void updateRecord(fstream&);
void newRecord(fstream&);
void deleteRecord(fstream&);
void outputLine(ostream&, const ClientData&);
int getAccount(const char* const);

int main() {
    // open file for reading and writing
    fstream inOutCredit("credit.dat", ios::in | ios::out | ios::binary);

    // exit program if fstream cannot open file
    if (!inOutCredit) {
        cerr << "File could not be opened." << endl;
        exit(EXIT_FAILURE);
    }

    Choice choice; // store user choice
    // enable user to specify action
    while ((choice = enterChoice()) != Choice::END) {
        switch (choice) {
            case Choice::PRINT: // create text file from record file
                createTextFile(inOutCredit);
                break;
            case Choice::UPDATE: // update record
                updateRecord(inOutCredit);
                break;
            case Choice::NEW: // create record
                newRecord(inOutCredit);
                break;
            case Choice::DELETE: // delete existing record
                deleteRecord(inOutCredit);
                break;
            default: // display error if user does not select valid choice
                cerr << "Incorrect choice" << endl;
                break;
        }
    }
    inOutCredit.clear(); // reset end-of-file indicator
}
```

Fig. 14.13 | 银行账户程序。（第2部分，共6部分。）

## 14.11 案例研究：事务处理程序 679
