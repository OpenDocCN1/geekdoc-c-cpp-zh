
```cpp
15 using std::ifstream;

16

17  #include <iomanip>

18  using std::setw;

19  using std::setprecision;

20

21  #include <string>

22  using std::string;

23

24  #include <cstdlib>

25  using std::exit; // exit 函数原型

26

27  enum RequestType { ZERO_BALANCE = 1, CREDIT_BALANCE, DEBIT_BALANCE, END };
  int getRequest();
  bool shouldDisplay( int, double );
  void outputLine( int, const string, double );

  int main()
  {
      // ifstream 构造函数打开文件
      ifstream inClientFile( "clients.dat", ios::in );

      // 如果 ifstream 未能打开文件则退出程序
      if ( !inClientFile )
      {
          cerr << "File could not be opened" << endl;
          exit( 1 );
      } // end if

      int request;
      int account;
      char name[ 30 ];
      double balance;

      // 获取用户的请求（例如零、信用或借记余额）
      request = getRequest();

      // 处理用户的请求
      while ( request != END )
      {
          switch ( request )
          {
              case ZERO_BALANCE:
                  cout << "\nAccounts with zero balances:\n";
                  break;
              case CREDIT_BALANCE:
                  cout << "\nAccounts with credit balances:\n";
                  break;
              case DEBIT_BALANCE:
                  cout << "\nAccounts with debit balances:\n";
                  break;
          } // end switch

      // 从文件中读取 account、name 和 balance
      inClientFile >> account >> name >> balance;
```
```
```
70

71     // 显示文件内容（直到 eof）
    while ( !inClientFile.eof() )
    {
        // 显示记录
        if ( shouldDisplay( request, balance ) )
            outputLine( account, name, balance );

        // 从文件中读取 account、name 和 balance
        inClientFile >> account >> name >> balance;
    } // end inner while

    inClientFile.clear(); // 为下一次输入重置 eof
    inClientFile.seekg( 0 ); // 重新定位到文件开头
    request = getRequest(); // 从用户获取额外请求
    } // end outer while

    cout << "End of run." << endl;
    return 0; // ifstream 析构函数关闭文件
} // end main

    // 从用户获取请求
int getRequest()
{
    int request; // 用户请求

    // 显示请求选项
    cout << "\nEnter request" << endl
        << " 1 - List accounts with zero balances" << endl
        << " 2 - List accounts with credit balances" << endl
        << " 3 - List accounts with debit balances" << endl
        << " 4 - End of run" << fixed << showpoint;

    do // 输入用户请求
    {
        cout << "\n? ";
        cin >> request;
    } while ( request < ZERO_BALANCE && request > END );

    return request;
} // end function getRequest

    // 确定是否显示给定记录
bool shouldDisplay( int type, double balance )
{
    // 确定是否显示零余额
    if ( type == ZERO_BALANCE && balance == 0 )
        return true;

    // 确定是否显示信用余额
    if ( type == CREDIT_BALANCE && balance < 0 )
        return true;
```
123   // determine whether to display debit balances
124   if ( type == DEBIT_BALANCE && balance > 0 )
125       return true;
126
127   return false;
128 } // end function shouldDisplay
129
130 // display single record from file
131 void outputLine( int account, const string name, double balance )
132 {
133     cout << left << setw( 10 ) << account << setw( 13 ) << name
134         << setw( 7 ) << setprecision( 2 ) << right << balance << endl;
135 } // end function outputLine
```

Enter request

1 - List accounts with zero balances

2 - List accounts with credit balances

3 - List accounts with debit balances

4 - End of run

? 1

Accounts with zero balances:

300      White            0.00

Enter request

1 - List accounts with zero balances

2 - List accounts with credit balances

3 - List accounts with debit balances

4 - End of run

? 2

Accounts with credit balances:

400      Stone           -42.16

Enter request

1 - List accounts with zero balances

2 - List accounts with credit balances

3 - List accounts with debit balances

4 - End of run

? 3

Accounts with debit balances:

100      Jones           24.98

200      Doe            345.67

500      Rich           224.62

Enter request

1 - List accounts with zero balances

2 - List accounts with credit balances

3 - List accounts with debit balances

4 - End of run

? 4

End of run.

## 17.6 更新顺序文件

如第 17.4 节所示以格式化方式写入顺序文件的数据，若要修改则有破坏文件中其他数据的风险。例如，如果需要将姓名“White”更改为“Worthington”，就无法在不破坏文件的情况下覆盖旧姓名。White 的记录写入文件时为

```
300 White 0.00
```

如果使用更长的姓名从文件中的同一位置重写该记录，则记录将变为

```
300 Worthington 0.00
```

新记录比原始记录多出六个字符。因此，“Worthington”中第二个“o”之后的字符将覆盖文件中下一个顺序记录的开头。问题在于，在使用流插入运算符 `<<` 和流提取运算符 `>>` 的格式化输入/输出模型中，字段——从而记录——大小可能变化。例如，值 7、14、−117、2074 和 27383 都是 `int`，在内部存储相同数量的“原始数据”字节（在当今流行的 32 位机器上通常为四个字节）。然而，这些整数作为格式化文本输出时成为不同大小的字段。因此，格式化输入/输出模型通常不用于原地更新记录。

这种更新可以笨拙地完成。例如，为了进行上述姓名更改，可以将 300 White 0.00 之前的记录复制到新文件，然后将更新后的记录写入新文件，再将 300 White 0.00 之后的记录复制到新文件。这需要处理文件中的每条记录才能更新一条记录。如果一次更新多条记录，则这种技术是可以接受的。

## 17.7 随机访问文件

到目前为止，我们已经了解了如何创建顺序文件并搜索它们以定位信息。顺序文件对于 *即时访问应用* 不合适，即必须立即定位特定记录的应用。常见的即时访问应用是航空公司预订系统、银行系统、销售点系统、自动取款机和其他需要快速访问特定数据的 *事务处理系统*。一家银行可能有数十万甚至数百万其他客户，但当客户使用自动取款机时，程序会在几秒钟或更短时间内检查该客户的账户是否有足够资金。这种即时访问是通过 *随机访问文件* 实现的。随机访问文件的单个记录可以直接（并且快速）访问，而无需搜索其他记录。

正如我们所说，C++ 不对文件施加结构。因此，想要使用随机访问文件的应用程序必须自行创建。可以使用多种技术。也许最简单的方法是要求文件中所有记录长度相同。使用相同大小的固定长度记录，使得程序能够根据记录大小和记录键计算出相对于文件开头的任何记录的确 exact 位置。我们很快就会看到这如何促进对大文件中特定记录的即时访问。

图 17.9 说明了 C++ 对由固定长度记录组成的随机访问文件的视图（在此情况下，每条记录长 100 字节）。随机访问文件就像一列火车，有许多相同大小的车厢——有些空着，有些装有内容。

可以在不破坏文件中其他数据的情况下向随机访问文件插入数据。之前存储的数据也可以在不重写整个文件的情况下进行更新或删除。在接下来的几节中，我们将解释如何创建随机访问文件，向文件中输入数据，以顺序和随机方式读取数据，更新数据以及删除不再需要的数据。

## 17.8 创建随机访问文件

`ostream` 成员函数 `write` 输出固定数量的字节，从内存中的特定位置开始，输出到指定的流。当流与文件关联时，函数 `write` 将数据写入文件由“put”文件位置指针指定的位置。`istream` 成员函数 `read` 从指定流中输入固定数量的字节到内存中从指定地址开始的区域。如果流与文件关联，函数 `read` 将在文件由“get”文件位置指针指定的位置输入字节。

### 使用 ostream 成员函数 write 写入字节

写入整数到文件时，而不是使用语句

```
outFile << number;
```

对于一个四字节的整数，该语句可能打印的位数最少为一位，最多为 11 位（10 位数字加一个符号，每个占用一个字节存储），我们可以使用语句

```
outFile.write( reinterpret_cast< const char * >( &number ),
    sizeof( number ) );
```

该语句始终写入整数的二进制版本的四个字节（在整数为四字节的机器上）。函数 `write` 将其第一个参数视为一组字节，通过将内存中的对象视为 `const char *`，即指向字节的指针。函数 `write` 从该位置开始输出其第二个参数指定的字节数——一个类型为 `size_t` 的整数。如我们将看到的，`istream` 函数 `read` 随后可用于将四个字节读回整数变量 `number`。

![](img/4fc2e1ee5600ca1ada5e16b9e1397269_712_0.png)

图 17.9 | C++ 对随机访问文件的视图。

### 使用 `reinterpret_cast` 运算符在指针类型之间转换

不幸的是，我们传递给函数 `write` 作为第一个参数的大多数指针都不是 `const char *` 类型。为了输出其他类型的对象，我们必须将指向这些对象的指针转换为 `const char *` 类型；否则，编译器将不会编译对函数 `write` 的调用。C++ 提供了 `reinterpret_cast` 运算符，用于在指针类型必须转换为不相关指针类型的情况。您也可以使用此转换运算符在指针和整数类型之间以及反之亦然进行转换。如果没有 `reinterpret_cast`，输出整数 `number` 的 `write` 语句将无法编译，因为编译器不允许将类型为 `int *` 的指针（表达式 `&number` 返回的类型）传递给期望 `const char *` 类型参数的函数——就编译器而言，这些类型不兼容。

`reinterpret_cast` 在编译时执行，不会改变其操作数指向的对象的数值。相反，它要求编译器将操作数重新解释为目标类型（在关键字 `reinterpret_cast` 之后尖括号中指定的类型）。在图 17.2 中，我们使用 `reinterpret_cast` 将 `ClientData` 指针转换为 `const char *`，从而将 `ClientData` 对象重新解释为要输出到文件的一组字节。随机访问文件处理程序很少写入单个字段到文件。通常，它们一次写入一个类的一个对象，如以下示例所示。

> **错误预防提示 17.1**
> 
> 使用 `reinterpret_cast` 很容易执行危险的操作，可能导致严重的执行时错误。
> **可移植性提示 17.1**
> 
> 使用 `reinterpret_cast` 取决于编译器，可能导致程序在不同平台上表现不同。`reinterpret_cast` 运算符不应在绝对必要时以外使用。
> **可移植性提示 17.2**
> 
> 读取未格式化数据（由 `write` 写入）的程序必须在与写入数据的程序兼容的系统上编译和执行，因为不同系统可能以不同方式表示内部数据。

### 信用处理程序

考虑以下问题陈述：

> 创建一个信用处理程序，能够为最多可容纳 100 个客户的公司存储最多 100 条固定长度记录。每条记录应由作为记录键的账号、姓氏、名字和余额组成。程序应能够更新账户、插入新账户、删除账户并将所有账户记录插入到格式化的文本文件中以便打印。

接下来的几节介绍了创建此信用处理程序的技术。图 17.12 说明了打开随机访问文件、使用 `ClientData` 类的对象（图 17.10–17.11）定义记录格式并以二进制格式将数据写入磁盘。此程序使用函数 `write` 将文件 `credit.dat` 的全部 100 条记录初始化为空对象。每个空对象包含账号为 0、姓氏和名字为空字符串（用空引号表示）以及余额为 0.0。每条记录都用将存储账户数据的空闲空间量进行初始化。

// Fig. 17.10: ClientData.h
// Class ClientData definition used in Fig. 17.12-Fig. 17.15.

#ifndef CLIENTDATA_H
#define CLIENTDATA_H

#include <string>
using std::string;

class ClientData
{
public:
    // default ClientData constructor
    ClientData( int = 0, string = "", string = "", double = 0.0 );
