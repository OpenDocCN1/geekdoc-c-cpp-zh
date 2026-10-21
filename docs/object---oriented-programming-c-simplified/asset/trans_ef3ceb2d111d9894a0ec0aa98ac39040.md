

返回非零值以指示严重的 I/O 错误。这与设置 badbit 错误状态相同。在此情况下不要继续在流上进行 I/O 操作。

## 3. The fail Function

```
SYNTAX : int fail ( ) const;
```

如果发生任何 I/O 错误（非文件结束），则返回非零值。此条件对应于 badbit 或 failbit 错误标志被设置。如果对 bad 的调用返回 0，则可以假设错误条件是非致命的，并且在清除标志后您可能可以继续处理。

## 4. The clear Function

```
SYNTAX : void clear (int nState = 0);
```

参数 nState，如果为 0，则清除所有错误位，否则根据以下掩码（ios 枚举器）设置位，这些掩码可使用按位或（|）运算符组合。nState 参数必须具有以下值之一：

- ios :: goodbit          无错误条件（无位被设置）。
- ios :: eofbit           已到达文件末尾。
- ios :: failbit          可能可恢复的格式化或转换错误。
- ios :: badbit           严重的 I/O 错误。

该函数设置或清除错误状态标志。rdstate 函数可用于读取当前错误状态。

## 5. The eof( ) Function

```
SYNTAX : int eof( ) const;
```

如果已到达文件末尾，则返回非零值。这与设置 eofbit 错误标志相同。

## 6. The rdstate Function

```
SYNTAX : int rdstate ( ) const;
```

返回当前错误状态，如以下掩码（ios 枚举器）所指定。

- ios :: goodbit          无错误条件（无位被设置）。
- ios :: eofbit           已到达文件末尾。
- ios :: failbit          可能可恢复的格式化或转换错误。
- ios :: badbit           严重的 I/O 错误或未知状态。

这在下面给出的图中显示。最后 4 位未使用。

返回的值可以用 AND (&) 运算符与掩码进行测试，但我们不必这样做，因为我们可以拥有告诉我们哪个位被设置或复位的函数。

![](img/ad5299318df8d4d7c6df5eaa86590ea3_623_0.png)

/* PROG 12.28 ERROR HANDLING WITH FILES */

#include <iostream.h>
#include <conio.h>
#include <fstream.h>
void main( )
{
        clrscr( );
        ofstream file("silly.txt", ios :: noreplace);
        if(!file)
        {
                cout << "FILE OPENING ERROR";
                endl(cout);
        }
        cout << "THE VARIOUS FLAGS SET/ RESET ARE";
        endl(cout);
        cout << "rdstate=" << file.rdstate( );
        endl(cout);
        cout << "bad=" << file.bad( );
        endl(cout);
        cout << "fail=" << file.fail( );
        endl(cout);
        cout << "good=" << file.good( );
        endl(cout);
        cout << "eof=" << file.eof( );
        endl(cout);
        getch( );
}

OUTPUT :
FILE OPENING ERROR
THE VARIOUS FLAGS SET/ RESET ARE
rdstate=2
bad=0
fail=2
good=0
eof=0

**EXPLANATION :** 文件 silly.txt 之前已存在。noreplace 在文件已存在且我们尝试以写入方式打开它时引发错误。也就是说，使用此标志我们可以知道文件已存在并且我们不必修改文件。文件打开错误发生，因此 fail 将返回非零值，good 仅在没有任何类型的错误发生时才返回 1 *i.e.*, 所有

位都被清除。bad 返回 0 因为没有 I/O 错误。未到达 eof，因此 eof 返回 0。现在根据图检查，rdstate 将为：

![](img/ad5299318df8d4d7c6df5eaa86590ea3_625_0.png)

Figure 12.16. Logical Implementation of rdstate( )

# 0010 是十进制 2，所以 rdstate 返回 2。

在程序中如果文件未打开且我们尝试向文件写入，则函数 bad 返回 true 且 badbit 表示文件输入/输出错误。这可以再次检查如下：

```
file << "WRITING TO THE FILE" << endl;
if(!file)
{
    cout << "WRITING ERROR";
    endl(cout);
}
//check all flags here;
```

```
/*PROG 12.29 DEMO OF FAIL AND GOOD */

#include <iostream.h>
#include <fstream.h>
#include <conio.h>
void main()
{
    clrscr();
    ifstream file("num.txt",ios ::nocreate);
    if(file.good())
    {
        cout << "File is opened successfully" << endl;
        cout << "good flag :=" << file.good() << endl;
    }
    else if(file.fail())
    {
        cout << "Error in opening file \n";
        cout << "Fail flag :=" << file.bad() << endl;
    }
}

OUTPUT :
File is opened successfully
good flag := 1
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_626_0.png)

Figure 12.17. Showing the output screen of the program 12.29.

EXPLANATION : 该程序是自解释的。

## 12.10 PONDERABLE POINTS

- 1. 打开文件将程序与文件链接起来。链接是通过 fstream、ifstream、ofstream 等文件流类的对象建立的，这些类在头文件 fstream.h 中定义。
- 2. 使用库函数访问的文件称为高级文件，而通过系统调用访问的文件称为低级文件。系统调用是对操作系统的特殊命令，并且指定给特定的操作系统。
- 3. 高级文件也称为流式文件，低级文件也称为系统定向文件。
- 4. 一般来说有两种类型的流
  - (a) 文本流，即字节序列（文本行）。
  - (b) 二进制流，即未处理的字节序列。
- 5. 通常所有文件都是以文本模式打开和访问的。为打开文件，需要指定二进制模式 ios :: binary mode。
- 6. 打开文件可以使用构造函数方法或 open 函数。
- 7. 各种模式如 ios :: in、ios :: out、ios :: ate 等是 ios 类的枚举常量。
- 8. 用于处理错误的各种函数有 good、bad、clear 等。

## EXERCISE

### A. True and False :

- 1. read( ) 和 write( ) 方法用于字符输入和输出。
- 2. fstream 只能用于读取数据。
- 3. read 和 write 函数用于从/向文件读取和写入对象。
- 4. 一个流可能同时连接到多个文件。

### B. Answer the Following Questions :

- 1. C++ 提供哪些不同类型的文件流？
- 2. 为什么我们需要 fstream 头文件？
- 3. 文件的优点是什么？
- 4. 文本文件与二进制文件有何不同？
- 5. 讨论文件的随机访问函数。
- 6. 打开模式有哪些？解释每种模式的目的。
- 7. 什么是命令行参数？我们在程序中如何使用它们？
- 8. 如何从/向文件读写对象？
- 9. C++ 提供了哪些各种错误处理函数？
- 10. 什么是 eof？如何检测文件结束？

### C. Brain Drill :

- 1. 编写一个程序，将文本文件的内容逐行反向显示在屏幕上。应可以通过提供文件名作为命令行参数来运行您的程序。
- 2. 编写一个 C++ 类来读取现有文件并创建另一个文件，其中包含源文件的所有单词以相反的顺序存储。假设连续的单词由一个或多个空白字符分隔。
- 3. 编写一个 C++ 程序来比较通过命令行提供的两个文件的内容。显示第一个不匹配的行及其行号。
- 4. 编写一个 C++ 程序，将源文件的交替行以相反的顺序复制到目标文件，文件名在命令提示符下输入。
- 5. 编写一个程序来模拟 DOS COPY 命令。也就是说，它应将文本文件（例如任何 .CPP 文件）的内容复制到另一个文件。用两个命令行参数调用该程序——源文件和目标文件，如下所示：
  C>copy srcfile.cpp destfile.cpp
  在程序中，检查用户是否输入了正确数量的命令行参数，并且指定的文件可以打开。
- 6. 编写一个程序，返回在命令行输入的程序的字节大小：
  C>filesize program.exe
- 7. 在循环中，提示用户输入名称数据，包括名字、中间名首字母、姓氏和员工编号（类型为 unsigned long）。然后，使用带插入（<<）运算符的格式化 I/O，将这四个数据项写入 ofstream 对象。不要忘记字符串必须以空格或其他空白字符终止。当用户指示不再输入名称数据时，关闭 ofstream 对象，打开 ifstream 对象，读取并显示文件中的所有数据，然后终止程序。
- 8. 创建一个 time 类，其中包含小时、分钟和秒的整数成员值。制作一个成员函数 get_time ( ) 从用户获取时间值，以及一个函数 put_time ( ) 以 12 :59 :59 格式显示时间。向 get_time ( ) 函数添加错误检查以最大限度地减少用户错误。此函数应分别请求小时、分钟和秒，并检查每个值是否具有 ios 错误状态标志和正确的范围。小时应在 0 到 23 之间，分钟和秒在 0 到 59 之间。不要将这些值作为字符串输入然后转换它们；直接作为整数读取。这意味着您将无法筛选出带有多余小数点的条目。
  在 main ( ) 中，使用循环重复使用 get_time ( ) 从用户获取时间值，然后使用 put_time ( ) 显示它，如下所示：
  Enter hours : 11
  Enter minutes : 59
  Enter seconds : 59
  Time = 11 :59 :59
  Do another (y/n) ? y

