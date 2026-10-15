

每个流对象都包含一组 *状态位*，用于控制流的状态（即格式化、设置错误状态等）。这些位由流的重载的 void * 强制转换运算符使用，以确定返回非空指针还是空指针。流提取操作会在输入错误类型的数据时设置流的 *failbit*，并在操作失败时设置流的 *badbit*。第 15.7 节和第 15.8 节详细讨论了流状态位，然后展示如何在 I/O 操作后测试这些位。

## 15.4.1 get 和 getline 成员函数

无参数的 *get* 成员函数从指定流中输入一个字符（包括空白字符和其他非图形字符，例如表示文件结束的键序列），并将其作为函数调用的值返回。get 的这个版本在流中遇到文件结束时会返回 EOF。

## 使用成员函数 eof、get 和 put

图 15.4 演示了在输入流 cin 上使用成员函数 eof 和 get，以及在输出流 cout 上使用成员函数 put。程序首先打印 cin.eof() 的值——即 false（输出为 0）——以显示 cin 上尚未发生文件结束。用户输入一行文本并按 Enter，然后输入文件结束（Microsoft Windows 系统上为 <Ctrl>-z，UNIX 和 Macintosh 系统上为 <Ctrl>-d）。第 17 行读取每个字符，第 18 行使用成员函数 put 将其输出到 cout。当遇到文件结束时，while 语句结束，第 22 行显示 cin.eof() 的值，此时为 true（输出为 1），以显示 cin 上已设置文件结束。请注意，此程序使用的是不带参数的 istream 成员函数 get 的版本并返回正在输入的字符（第 17 行）。函数 eof 只有在程序尝试读取流中最后一个字符之后才会返回 true。

```
1  // Fig. 15.4: Fig15_04.cpp
2  // Using member functions get, put and eof.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  int main()
9  {
10     int character; // use int, because char cannot represent EOF
11
12     // prompt user to enter line of text
13     cout << "Before input, cin.eof() is " << cin.eof() << endl
14        << "Enter a sentence followed by end-of-file:" << endl;
15
16     // use get to read each character; use put to display it
17     while ( ( character = cin.get() ) != EOF )
18         cout.put( character );
19
20     // display end-of-file character
21     cout << "\nEOF in this system is: " << character << endl;
22     cout << "After input of EOF, cin.eof() is " << cin.eof() << endl;
23     return 0;
24 } // end main
```

Fig. 15.4 | get, put and eof member functions. (Part 1 of 2.)

```
Before input, cin.eof() is 0
Enter a sentence followed by end-of-file:
Testing the get and put member functions
Testing the get and put member functions
^Z

EOF in this system is: -1
After input of EOF, cin.eof() is 1
```

Fig. 15.4 | get, put and eof member functions. (Part 2 of 2.)

带字符引用参数的 get 成员函数从输入流中输入下一个字符（即使是空白字符），并将其存储在字符参数中。get 的这个版本返回调用 get 成员函数的 istream 对象的引用。

get 的第三个版本接受三个参数——字符数组、大小限制和分隔符（默认值 '\n'）。这个版本从输入流中读取字符。它要么读取少于指定最大字符数的一个字符并终止，要么在读取到分隔符时终止。空字符被插入到用作程序缓冲区的字符数组中以终止输入字符串。分隔符不被放置在字符数组中，但仍保留在输入流中（分隔符将是读取的下一个字符）。因此，第二次连续的 get 的结果为空行，除非分隔符字符从输入流中移除（可能使用 cin.ignore()）。

## 比较 cin 和 cin.get

图 15.5 比较了使用流提取的 cin 输入（读取字符直到遇到空白字符）和使用 cin.get 输入。注意对 cin.get 的调用（第 24 行）未指定分隔符，因此使用默认的 '\n' 字符。

```
1  // Fig. 15.5: Fig15_05.cpp
2  // Contrasting input of a string via cin and cin.get.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  int main()
9  {
10   // create two char arrays, each with 80 elements
11   const int SIZE = 80;
12   char buffer1[ SIZE ];
13   char buffer2[ SIZE ];
14
15  // use cin to input characters into buffer1
16  cout << "Enter a sentence:" << endl;
17  cin >> buffer1;
18
19  // display buffer1 contents
20  cout << "\nThe string read with cin was:" << endl
21      << buffer1 << endl << endl;
22
23  // use cin.get to input characters into buffer2
24  cin.get( buffer2, SIZE );
25
26  // display buffer2 contents
27  cout << "The string read with cin.get was:" << endl
28      << buffer2 << endl;
29      return 0;
30  } // end main
```

Fig. 15.5 | Input of a string using cin with stream extraction contrasted with input using cin.get. (Part 1 of 2.)

Enter a sentence:
**Contrasting string input with cin and cin.get**

The string read with cin was:
Contrasting

The string read with cin.get was:
string input with cin and cin.get

Fig. 15.5 | Input of a string using cin with stream extraction contrasted with input using cin.get. (Part 2 of 2.)

## 使用成员函数 getline

成员函数 getline 的操作与 get 成员函数的第三个版本类似，并在字符数组中的行后插入空字符。getline 函数会从流中移除分隔符（即读取该字符并丢弃它），但不将其存储在字符数组中。图 15.6 的程序演示了使用 getline 成员函数输入一行文本（第 15 行）。

```
1  // Fig. 15.6: Fig15_06.cpp
2  // Inputting characters using cin member function getline.
3  #include <iostream>
4  using std::cin;
5  using std::cout;
6  using std::endl;
7
8  int main()
9  {
10     const int SIZE = 80;
11     char buffer[ SIZE ]; // create array of 80 characters
12
```

Fig. 15.6 | Inputting character data with cin member function getline. (Part 1 of 2.)

输出流并跳过输入流中的空白。这些功能在以下各节中描述。

## 15.6.1 整数流基数：dec、oct、hex 和 setbase

整数通常按十进制（基数 10）值解释。要更改流中整数的解释基数，插入 hex 操纵符将基数设置为十六进制（基数 16），或插入 oct 操纵符将基数设置为八进制（基数 8）。插入 dec 操纵符可将流基数重置为十进制。这些都是粘性操纵符。

流的基数也可以通过 setbase 流操纵符更改，该操纵符接受一个整数参数 10、8 或 16，分别将基数设置为十进制、八进制或十六进制。因为 setbase 接受参数，所以它被称为参数化流操纵符。使用 setbase（或其他任何参数化操纵符）需要包含 <iomanip> 头文件。流基数值保持不变，直到明确更改；setbase 设置是“粘性”的。图 15.8 演示了流操纵符 hex、oct、dec 和 setbase。

```
// Fig. 15.8: Fig15_08.cpp
// Using stream manipulators hex, oct, dec and setbase.
#include <iostream>
using std::cin;
using std::cout;
using std::dec;
using std::endl;
using std::hex;
using std::oct;

#include <iomanip>
using std::setbase;

int main()
{
    int number;

    cout << "Enter a decimal number: ";
    cin >> number; // input number

    // use hex stream manipulator to show hexadecimal number
    cout << number << " in hexadecimal is: " << hex
         << number << endl;

    // use oct stream manipulator to show octal number
    cout << dec << number << " in octal is: "
         << oct << number << endl;

    // use setbase stream manipulator to show decimal number
    cout << setbase( 10 ) << number << " in decimal is: "
         << number << endl;
    return 0;
} // end main
```

Fig. 15.8 | Stream manipulators hex, oct, dec and setbase. (Part 1 of 2.)

