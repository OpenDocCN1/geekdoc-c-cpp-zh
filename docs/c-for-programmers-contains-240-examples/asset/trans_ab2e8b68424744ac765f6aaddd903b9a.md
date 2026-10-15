
![](img/4fc2e1ee5600ca1ada5e16b9e1397269_719_0.png)

**图 17.13** | 写入随机访问文件。（第 3 部分，共 3 部分。）

第 59–60 行将对象 `outCredit` 的“put”文件位置指针定位到通过以下公式计算出的字节位置：

```cpp
( client.getAccountNumber() - 1 ) * sizeof( ClientData )
```

由于账户编号在 1 到 100 之间，因此在计算记录的字节位置时，会从账户编号中减去 1。因此，对于记录 1，文件位置指针设置为文件的字节 0。请注意，第 28 行使用 fstream 对象 `outCredit` 打开现有的 `credit.dat` 文件。通过组合文件打开模式 `ios::in`、`ios::out` 和 `ios::binary`，以二进制模式打开该文件进行输入和输出。多个文件打开模式是通过将每个打开模式与下一个打开模式用按位或运算符（`|`）分隔来组合的。以这种方式打开现有的 `credit.dat` 文件，可确保此程序能够操作图 17.12 的程序写入该文件的记录，而不是从头创建该文件。第 19 章“位、字符、C 字符串和结构体”详细讨论了按位或运算符。

## 17.10 顺序读取随机访问文件

在前面的章节中，我们创建了一个随机访问文件并向该文件写入了数据。在本节中，我们将开发一个程序，该程序顺序读取文件，并且只打印包含数据的记录。这些程序还带来了额外的好处。看看你是否能确定它是什么；我们将在本节末尾揭示它。

`istream` 函数 `read` 从指定流的当前位置开始，将指定数量的字节输入到一个对象中。例如，图 17.14 中的第 57–58 行从与 `ifstream` 对象 `inCredit` 关联的文件中读取 `sizeof( ClientData )` 指定的字节数，并将数据存储在客户记录中。请注意，函数 `read` 要求第一个参数为 `char *` 类型。由于 `&client` 的类型是 `ClientData *`，必须使用强制转换运算符 reinterpret_cast 将 &client 转换为 char *。请注意，第 24 行包含了图 17.10 中定义的头文件 ClientData.h，因此程序可以使用 ClientData 对象。

图 17.14 顺序读取 credit.dat 文件中的每条记录，检查每条记录以确定它是否包含数据，并对包含数据的记录显示格式化输出。第 50 行的条件使用 ios 成员函数 eof 来确定何时到达文件末尾，并导致 while 语句的执行终止。此外，如果从文件读取时发生错误，循环也会终止，因为 inCredit 的计算结果为 false。从文件输入的数据由函数 outputLine（第 65–72 行）输出，该函数接受两个参数——一个 ostream 对象和一个要输出的 clientData 结构。ostream 参数类型很有趣，因为任何 ostream 对象（如 cout）或任何 ostream 派生类的对象（如 ofstream 类型的对象）都可以

```
// Fig. 17.14: Fig17_14.cpp
// Reading a random-access file sequentially.
#include <iostream>
using std::cerr;
using std::cout;
using std::endl;
using std::fixed;
using std::ios;
using std::left;
using std::right;
using std::showpoint;

#include <iomanip>
using std::setprecision;
using std::setw;

#include <fstream>
using std::ifstream;
using std::ostream;

#include <cstdlib>
using std::exit; // exit function prototype

#include "ClientData.h" // ClientData class definition

void outputLine( ostream&, const ClientData & ); // prototype

int main()
{
    ifstream inCredit( "credit.dat", ios::in | ios::binary );

    // exit program if ifstream cannot open file
    if ( !inCredit )
    {
        cerr << "File could not be opened." << endl;
        exit( 1 );
    } // end if
```

```cpp
cout << left << setw( 10 ) << "Account" << setw( 16 )
     << "Last Name" << setw( 11 ) << "First Name" << left
     << setw( 10 ) << right << "Balance" << endl;

ClientData client; // create record

// read first record from file
inCredit.read( reinterpret_cast< char * >( &client ),
               sizeof( ClientData ) );

// read all records from file
while ( inCredit && !inCredit.eof() )
{
   // display record
   if ( client.getAccountNumber() != 0 )
      outputLine( cout, client );

   // read next from file
   inCredit.read( reinterpret_cast< char * >( &client ),
                  sizeof( ClientData ) );
} // end while

return 0;
} // end main

// display single record
void outputLine( ostream &output, const ClientData &record )
{
   output << left << setw( 10 ) << record.getAccountNumber()
          << setw( 16 ) << record.getLastName()
          << setw( 11 ) << record.getFirstName()
          << setw( 10 ) << setprecision( 2 ) << right << fixed
          << showpoint << record.getBalance() << endl;
} // end function outputLine
```

| 账户 | 姓氏 | 名字 | 余额 |
|---:|---|---|---:|
| 29 | Brown | Nancy | -24.54 |
| 33 | Dunn | Stacey | 314.33 |
| 37 | Barker | Doug | 0.00 |
| 88 | Smith | Dave | 258.34 |
| 96 | Stone | Sam | 34.98 |

图 17.14 | 顺序读取随机访问文件。（第 2 部分，共 2 部分。）

作为参数提供。这意味着，例如，同一个函数可以用于向标准输出流和文件流执行输出，而无需编写单独的函数。

我们承诺的额外好处呢？如果你检查输出窗口，你会注意到记录是按账户编号排序的。这是我们使用直接访问技术将记录存储在文件中的结果。与我们第 7 章中使用的插入排序相比，使用直接访问技术进行排序是

相对较快。这种速度是通过使文件足够大以容纳可能创建的每条记录来实现的。这当然意味着文件大部分时间可能被稀疏占用，导致存储浪费。这是空间-时间权衡的另一个例子：通过使用大量空间，我们能够开发出更快的排序算法。幸运的是，存储单元价格的持续下降使这个问题变得不那么严重。

## 17.11 案例研究：事务处理程序

我们现在介绍一个使用随机访问文件实现“即时”访问处理的大型事务处理程序（图 17.15）。该程序维护银行的账户信息。程序更新现有账户、添加新账户、删除账户，并将所有当前账户的格式化列表存储在一个文本文件中。我们假设图 17.12 中的程序已经执行以创建文件 credit.dat，图 17.13 中的程序已经执行以插入初始数据。

```cpp
// Fig. 17.15: Fig17_15.cpp
// This program reads a random-access file sequentially, updates
// data previously written to the file, creates data to be placed
// in the file, and deletes data previously stored in the file.
#include <iostream>
using std::cerr;
using std::cin;
using std::cout;
using std::endl;
using std::fixed;
using std::ios;
using std::left;
using std::right;
using std::showpoint;

#include <fstream>
using std::ofstream;
using std::ostream;
using std::fstream;

#include <iomanip>
using std::setw;
using std::setprecision;

#include <cstdlib>
using std::exit; // exit function prototype

#include "ClientData.h" // ClientData class definition

int enterChoice();
void createTextFile( fstream& );
void updateRecord( fstream& );
void newRecord( fstream& );
void deleteRecord( fstream& );
```

**图 17.15** | 银行账户程序。（第 1 部分，共 6 部分。）

```
void outputLine( ostream&, const ClientData & );
int getAccount( const char * const );

enum Choices { PRINT = 1, UPDATE, NEW, DELETE, END };

int main()
{
    // open file for reading and writing
    fstream inOutCredit( "credit.dat", ios::in | ios::out | ios::binary );

    // exit program if fstream cannot open file
    if ( !inOutCredit )
    {
        cerr << "File could not be opened." << endl;
        exit ( 1 );
    } // end if

    int choice; // store user choice

    // enable user to specify action
    while ( ( choice = enterChoice() ) != END )
    {
        switch ( choice )
        {
            case PRINT: // create text file from record file
                createTextFile( inOutCredit );
                break;
            case UPDATE: // update record
                updateRecord( inOutCredit );
                break;
            case NEW: // create record
                newRecord( inOutCredit );
                break;
            case DELETE: // delete existing record
                deleteRecord( inOutCredit );
                break;
            default: // display error if user does not select valid choice
                cerr << "Incorrect choice" << endl;
                break;
        } // end switch

        inOutCredit.clear(); // reset end-of-file indicator
    } // end while

    return 0;
} // end main

// enable user to input menu choice
int enterChoice()
{
    // display available options
    cout << "\nEnter your choice" << endl
         << "1 - store a formatted text file of accounts" << endl
```
