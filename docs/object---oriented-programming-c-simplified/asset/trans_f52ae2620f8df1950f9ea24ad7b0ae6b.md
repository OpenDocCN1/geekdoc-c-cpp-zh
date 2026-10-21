

## PROG 12.9 EOF 函数和追加模式的演示

```cpp
#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main()
{
    fstream rw;
    char str[100];
    clrscr();
    rw.open("demo.txt", ios::in);
    cout << "data read from file";
    endl(cout);
    while (rw.eof() != 0)
    {
        rw.getline(str, 100);
        cout << str << endl;
    }
    rw.close();
    rw.open("demo.txt", ios::app);
    cin.getline(str, 100);
    rw << str << endl;
    rw.close();
    rw.open("demo.txt", ios::in);
    cout << "File with append data \n";
    while (rw.eof() != 0)
    {
        rw.getline(str, 100);
        cout << str << endl;
    }
    rw.close();
    getch();
}
```

### OUTPUT

```
data read from file
This program for checking end of file
Hello C++
File with append data
This program for checking end of file
Hello C++
```

### EXPLANATION

文件 demo.txt 最初以读模式打开。只要我们仍在从文件中读取，函数 eof 就返回 0。一旦到达文件末尾，函数 eof 就返回非零值。我们一直从文件中读取，直到函数 eof 返回 0。在 while 循环的每次迭代中，我们读取一个最大长度为 99 字符的字符串 str。一旦遇到文件末尾，while 循环就终止。我们关闭文件并使用 ios::app 标志以追加模式打开文件。当文件以追加模式打开时，文件指针位于文件末尾。要追加到文件中的字符串从用户处获取并追加到文件中。文件再次关闭。接下来，文件以读模式打开并显示，这显示了追加的字符串以及追加前的原始内容。

## PROG 12.10 使用 GET 和 PUT 进行读写

```cpp
#include <iostream.h>
#include <fstream.h>
#include <stdio.h>
void main()
{
    fstream rw;
    char ch;
    rw.open("temp.txt", ios::in | ios::out);
    cout << "Enter some data" << endl;
    cin.get(ch);
    while (ch != EOF)
    {
        rw.put(ch);
        cin.get(ch);
    }
    rw.seekg(0, ios::beg);
    while (rw.eof() == 0)
    {
        cout.put(ch);
        rw.get(ch);
    }
    rw.close();
}
```

### OUTPUT

```
Enter some data
Hari Mohan Pandey faculty in CSE Dept.(Enter F6 or Ctrl+Z)^Z
Hari Mohan Pandey faculty in CSE Dept.(Enter F6 or Ctrl+Z)
```

### EXPLANATION

两个函数 put 和 get 使我们能够顺序读写文件。我们以读写方式打开文件 temp.txt。我们提示用户输入一些数据。数据使用 get 逐字符扫描并使用 put 一次一个字符写入文件。当用户输入 F6 或 Ctrl+Z 时，第一个 while 循环终止。然后通过编写 rw.seekg(0, ios::beg) 将指针移至文件开头。我们现在逐字符从文件中读取，直到到达文件末尾。EOF 是在文件 stdio.h 中定义的宏，其 ASCII 值为 26。

## PROG 12.11

```cpp
#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main()
{
    fstream source, dest;
    char sfile[15], dfile[15];
    char ch;
    clrscr();
    cout << "Enter the source file name" << endl;
    cin >> sfile;
    source.open(sfile, ios::in);
    cout << "Enter the destination file name" << endl;
    cin >> dfile;
    dest.open(dfile, ios::out);
    while (source.eof() == 0)
    {
        source.get(ch);
        dest.put(ch);
    }
    source.close();
    dest.close();
}
```

### OUTPUT

```
Enter the source file name
Hari.txt
Enter the destination file name
Pandey.txt
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_597_0.png)

*Figure 12.3. Output screen of program 12.11.*

### EXPLANATION

我们从用户输入源文件和目标文件名。假设源文件存在，因此我们在程序中没有加入任何错误检查代码。然后以读模式打开源文件，并以写模式打开目标文件。我们一次从源文件中读取一个字符并将其写入目标文件。这一直持续到到达源文件末尾。最后关闭两个文件。

## PROG 12.12 同时处理两个文件

```cpp
#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main()
{
    fstream f1, f2;
    clrscr();
    f1.open("names.txt", ios::out);
    f1 << "Hari" << endl;
    f1 << "Vijay" << endl;
    f1 << "Ranjana" << endl;
    f1.close();
    f2.open("sname.txt", ios::out);
    f2 << "Pandey" << endl;
    f2 << "Nath" << endl;
    f2 << "Pandey" << endl;
    f2.close();
    f1.open("names.txt", ios::in);
    f2.open("sname.txt", ios::in);
    char str[15];
    while (f1.eof() != 0)
    {
        f1.getline(str, 15);
        cout << str << " ";
        f2.getline(str, 15);
        cout << str << endl;
    }
    f1.close();
    f2.close();
}
```

### OUTPUT

```
Hari Pandey
Vijay Nath
Ranjana Pandey
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_598_0.png)

*Figure 12.4. Output Screen of program 12.12.*

### EXPLANATION

在程序中我们使用了两个文件 names.txt，其中我们存储了一些名字，以及 sname.txt，其中我们存储了姓氏。我们同时打开两个文件并显示全名。如果遇到第一个文件的末尾，我们终止程序。

## PROG 12.13 统计文件中的字符数

```cpp
#include <iostream.h>
#include <fstream.h>
#include <conio.h>
void main()
{
    fstream rw;
    char str[50];
    int count = 0;
    char ch;
    clrscr();
    rw.open("demo1.txt", ios::in);
    cout << "Data read from file" << endl;
    rw.get(ch);
    while (rw.eof() != 0)
    {
        cout.put(ch);
        rw.get(ch);
        count++;
    }
    cout << "Number of character in file := " << count << endl;
    rw.close();
}
```

### OUTPUT

```
Data read from file
MPSTME, NMIMS UNIVERSITY MUMBAI
HANDLING IN C
Number of character in file := 46
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_599_0.png)

*Figure 12.5. Output screen of program 12.13.*

### EXPLANATION

程序以读模式打开文件 demo1.txt。它逐字符读取文件，并在每次迭代中递增 count。退出 while 循环后，count 显示文件中的字符数。请注意，如果你通过手动计数字符来交叉检查输出，你需要为换行符额外加上 4 个。

## 12.6 文件中的随机访问

随机访问意味着从文件的任何位置随机读取数据。为此，我们首先需要在文件中设置文件指针的位置，然后再读取数据。C++ 文件流类为文件指针在文件中的操作提供了以下函数。借助这些函数，我们可以以随机方式访问数据。

- (a) Seekg( )
- (b) seekp( )
- (c) tellg( )
- (d) tellp( )

函数 seekg 和 tellg 在我们从文件中读取时使用，即与 get 指针一起使用；因此后缀为 g。函数 tellp 和 seekp 在写入文件时使用，即使用 put 指针；因此后缀为 p。seek (p/g) 函数将指针移动到指定位置，而 tell (p/g) 给出当前指针的位置。最常用的函数是 seekg，其语法如下：

```
istream & seekg (streamoff off, ios::seek_dir dir);
```

`off` 是新的偏移值，`streamoff` 是 `long` 的 typedef。 正偏移意味着向前移动，负值意味着向后移动，0 意味着停留在当前位置。文件中的第一个字节位于位置 0。`dir` 是搜索方向，必须是以下枚举器之一：

- ios::beg — 从流开头开始查找。
- ios::cur — 从流中的当前位置开始查找。
- ios::end — 从流末尾开始查找。

```
ifstream file;
file.seekg(2, ios::beg);   // 第三字节从开头开始。
file.seekg(6, ios::cur);   // 从当前位置向前 6 字节。
file.seekg(-5, ios::cur);  // 从当前位置向后 5 字节。
file.seekg(-4, ios::end);  // 从末尾向后 4 字节。
file.seekg(0, ios::cur);   // 停留在当前位置。
```

类似于 seekg，你可以使用 seekp 在打开用于写入的文件中移动指针。函数 tellg 和 tellp 可用于通过打开文件并将指针移动到文件末尾来查找文件中的字节数。它们可用于如下：

```
ofstream file("num.txt", ios::ate);
cout << file.tellp() << endl;
```

打开文件时指针将位于文件末尾，tellp 将给出文件中的字节数。同样，我们可以使用 tellg：

```
ifstream file("num.txt", ios::in);
file.seekg(0, ios::end);
cout << file.tellg() << endl;
```

打开文件以供读取时，文件指针将位于文件开头，因此我们使用 seekg 将指针移动到文件末尾。

让我们现在看几个使用这些函数的程序。

## PROG 12.14 反转文件内容

```cpp
#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main()
{
    fstream file;
    int count, x=1;
```
