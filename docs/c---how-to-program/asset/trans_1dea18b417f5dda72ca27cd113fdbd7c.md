
// Fig. 21.5: fig21_05.cpp
// Contrasting input of a string via cin and cin.get.
#include <iostream>
using namespace std;

int main()
{
    // create two char arrays, each with 80 elements
    const int SIZE = 80;
    char buffer1[ SIZE ];
    char buffer2[ SIZE ];

    // use cin to input characters into buffer1
    cout << "Enter a sentence:" << endl;
    cin >> buffer1;

    // display buffer1 contents
    cout << "\nThe string read with cin was:" << endl
         << buffer1 << endl << endl;

    // use cin.get to input characters into buffer2
    cin.get( buffer2, SIZE );

    // display buffer2 contents
    cout << "\nThe string read with cin.get was:" << endl
         << buffer2 << endl;
} // end main

Enter a sentence:
Contrasting string input with cin and cin.get

The string read with cin was:
Contrasting

The string read with cin.get was:
string input with cin and cin.get

图 21.5 | 对比使用 cin 和 cin.get 输入字符串。

## 使用成员函数 getline

成员函数 getline 的操作与 get 成员函数的第三个版本类似，并在内置 char 数组中该行之后插入一个空字符。getline 函数从流中移除分隔符（即读取该字符并丢弃它），但不将其存储到字符数组中。图 21.6 的程序演示了使用 getline 成员函数输入一行文本（第 13 行）。

// Fig. 21.6: fig21_06.cpp
// Inputting characters using cin member function getline.
#include <iostream>
using namespace std;

int main()
{
   const int SIZE = 80;
   char buffer[ SIZE ]; // create array of 80 characters

   // input characters in buffer via cin function getline
   cout << "Enter a sentence:" << endl;
   cin.getline( buffer, SIZE );

   // display buffer contents
   cout << "\nThe sentence entered is:" << endl << buffer << endl;
} // end main

图 21.6 | 使用 cin 成员函数 getline 输入字符。（第 I 部分，共 2 部分。）

Enter a sentence:
Using the getline member function

The sentence entered is:
Using the getline member function

**图 21.6**  |  使用 cin 成员函数 getline 输入字符。（第 2 部分，共 2 部分。）

### 21.4.2 istream 成员函数 peek、putback 和 ignore

istream 的 **ignore** 成员函数读取并丢弃指定数量的字符（默认为 *一个*），或在遇到指定分隔符时终止（默认为 EOF；当从文件读取时，这会使 ignore 跳到文件末尾）。

**putback** 成员函数将由 get 从输入流获得的前一个字符放回该流中。此函数对于扫描输入流以查找以特定字符开头的字段的应用程序很有用。当该字符被输入时，应用程序将该字符返回到流中，因此该字符可以包含在输入数据中。

**peek** 成员函数返回输入流中的下一个字符，但不从流中移除该字符。

### 21.4.3 类型安全的 I/O

C++ 提供类型安全的 I/O。<< 和 >> 运算符被重载以接受 *特定类型* 的数据项。如果处理了意外数据，就会设置各种错误位，用户可以测试这些错误位以确定 I/O 操作是成功还是失败。如果运算符 << 和 >> 未针对用户定义类型进行重载，而你试图输入或输出该用户定义类型对象的内容，编译器会报告错误。这使程序能够“保持控制”。我们将在 21.8 节讨论这些错误状态。

## 21.5 无格式 I/O（使用 read、write 和 gcount）

无格式输入/输出分别使用 istream 和 ostream 的 read 和 write 成员函数执行。成员函数 read 将 *字节* 输入到内存中的内置 char 数组；函数 write 从内置 char 数组输出字节。这些字节不以任何方式 *格式化*。它们作为原始字节输入或输出。例如，调用

char buffer[] = "HAPPY BIRTHDAY";
cout.write( buffer, 10 );

会输出 buffer 的前 10 个字节（包括空字符，如果有的话；这些空字符会导致使用 cout 和 << 的输出终止）。调用

cout.write( "ABCDEFGHIJKLMNOPQRSTUVWXYZ", 10 );

会显示字母表的前 10 个字符。

read 成员函数将指定数量的字符输入到内置 char 数组。如果读取的字符数少于指定数量，则设置 failbit。21.8 节说明如何确定 failbit 是否已设置。成员函数 gcount 报告最后一次输入操作读取的字符数。

图 21.7 演示了 istream 成员函数 read 和 gcount，以及 ostream 成员函数 write。该程序使用 read 将 20 个字符（来自更长的输入序列）输入到数组 buffer 中（第 13 行），使用 gcount 确定输入的字符数（第 17 行），并使用 write 输出 buffer 中的字符（第 17 行）。

// Fig. 21.7: fig21_07.cpp
// Unformatted I/O using read, gcount and write.
#include <iostream>
using namespace std;

int main()
{
   const int SIZE = 80;
   char buffer[ SIZE ]; // create array of 80 characters

   // use function read to input characters into buffer
   cout << "Enter a sentence:" << endl;
   cin.read( buffer, 20 );

   // use functions write and gcount to display buffer characters
   cout << endl << "The sentence entered was:" << endl;
   cout.write( buffer, cin.gcount() );
   cout << endl;
} // end main

Enter a sentence:
Using the read, write, and gcount member functions
The sentence entered was:
Using the read, writ

图 21.7 | 使用 read、gcount 和 write 的无格式 I/O。

## 21.6 流操纵器简介

C++ 提供各种执行格式化任务的流操纵器。流操纵器提供诸如设置字段宽度、设置精度、设置和取消设置格式状态、设置字段中的填充字符、刷新流、在输出流中插入换行符（并刷新流）、在输出流中插入空字符以及跳过输入流中的空白等功能。以下各节将描述这些特性。

### 21.6.1 整数流基数：dec、oct、hex 和 setbase

整数通常被解释为十进制（基数为 10）值。要更改流中整数的解释基数，可插入 hex 操纵器将基数设置为十六进制（基数为 16），或插入 oct 操纵器将基数设置为八进制（基数为 8）。插入 dec 操纵器可将流基数重置为十进制。这些都是粘性操纵器。

流基数也可以通过 setbase 流操纵器更改，它接受一个为 10、8 或 16 的 int 参数，分别将基数设置为十进制、八进制或十六进制。因为 setbase 接受一个参数，所以它被称为参数化流操纵器。像 setbase 这样的参数化流操纵器需要头文件 <iomanip>。流基数值保持不变，直到被显式更改；setbase 设置是粘性的。图 21.8 演示了流操纵器 hex、oct、dec 和 setbase。有关十进制、八进制和十六进制数的更多信息，请参见附录 C。

```cpp
// Fig. 21.8: fig21_08.cpp
// Using stream manipulators hex, oct, dec and setbase.
#include <iostream>
#include <iomanip>
using namespace std;

int main()
{
    int number;

    cout << "Enter a decimal number: ";
    cin >> number; // input number

    // use hex stream manipulator to show hexadecimal number
    cout << " number " << " in hexadecimal is: " << hex
         << number << endl;

    // use oct stream manipulator to show octal number
    cout << dec << number << " in octal is: "
         << oct << number << endl;

    // use setbase stream manipulator to show decimal number
    cout << setbase( 10 ) << number << " in decimal is: "
         << number << endl;
} // end main
```

Enter a decimal number: 20
20 in hexadecimal is: 14
20 in octal is: 24
20 in decimal is: 20

图 21.8 | 使用流操纵器 hex、oct、dec 和 setbase。

### 21.6.2 浮点精度（precision、setprecision）

我们可以通过使用 setprecision 流操纵器或 ios_base 的 precision 成员函数来控制浮点数的精度（即小数点右侧的位数）。调用其中任何一个都会为所有
