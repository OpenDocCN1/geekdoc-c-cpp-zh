

```cpp
fobj << " FILE HANDLING DEMO" << endl;
fobj.close();
getch();
}
```

**输出：**

(BLANK SCREEN)

**说明：** 该程序展示了另一种仅用于写入的打开文件的方法。它简单地创建了一个 `ofstream` 类类型的对象，并使用 `open` 方法打开文件。其余部分与前一个程序的解释相同。`open` 方法还有一个参数，用于指定我们希望以何种模式打开文件。这里写入的模式为 `ios::out`，但对于 `ofstream` 类来说这是可选的，因为默认情况下文件仅用于写入。

```cpp
/* PROG 12.3 DEMO OF FILE HANDLING, READING FROM FILE VER 1*/

#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main( )
{
    clrscr( );
    ifstream fobj;
    fobj.open("demo.txt");
    char str[30];
    fobj.getline(str,30);
    cout << "STRING READ FROM FILE" << endl;
    cout << str << endl;
    fobj.close( );
    getch( );
}
```

**输出：**

STRING READ FROM FILE
FILE HANDLING DEMO

**说明：** 语句 `ifstream fobj;` 创建了一个名为 `fobj` 的 `ifstream` 类型对象。类 `ifstream` 仅用于读取。我们使用 `open` 方法打开文件。想要打开的文件名作为参数传递给 `open` 方法。`open` 方法打开文件 `demo.txt` 并将对象 `fobj` 链接到此文件。现在此对象 `fobj` 作为从该文件 `demo.txt` 读取的流。我们按如下方式从文件中读取：

```cpp
fobj.getline(str,30);
```

上面的行从文件 `demo.txt` 读取前 29 个字符，或直到遇到 `\n` 为止的字符数。扫描到的字符串存储在 `str` 中，我们使用标准输出流 `cout` 将其显示在屏幕上。

请注意以下两行：

```cpp
ifstream fobj;
fobj.open("demo.txt");
```

可以写成：

```cpp
ifstream fobj("demo.txt");
```

正如我们对 `ofstream` 类所做的那样。

`open` 方法还有一个参数，用于指定我们希望以何种模式打开文件。这里读取的模式为 `ios::in`，但对于 `ifstream` 类来说这是可选的，因为默认情况下文件仅用于读取。

```cpp
/* PROG 12.4 WRITING PERSON DATA TO FILE */

#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main( )
{
    clrscr( );
    ofstream fobj;
    fobj.open("demo.txt");
    char name[25];
    int age;
    char sex;
    cout << "ENTER NAME HERE := ";
    cin.getline(name,25);
    cout << endl << "ENTER THE AGE AND SEX := ";
    cin >> age >> sex;
    fobj << name << endl << age << endl << sex << endl;
    fobj.close( );
    getch( );
}
```

**输出：**

ENTER NAME HERE := HARI MOHAN PANDEY
ENTER THE AGE AND SEX := 24 M

**说明：** 在程序中我们打开了一个文件 `demo.txt`。在文件中我们放置了个人的详细信息，即姓名、年龄和性别。我们从标准输入流（即键盘）获取输入并将扫描到的数据放入链接到对象 `fobj` 的文件 `demo.txt` 中。

| 编号 | 模式 | 描述 |
| --- | --- | --- |
| 1. | `ios::in` | 以读模式打开文件 |
| 2. | `ios::out` | 以写模式打开文件 |
| 3. | `ios::app` | 以追加模式打开文件 |
| 4. | `ios::trunc` | 如果文件已存在，则删除文件内容 |
| 5. | `ios::nocreate` | 如果文件不存在，打开函数将失败 |
| 6. | `ios::noreplace` | 如果文件已存在，则不打开文件 |
| 7. | `ios::binary` | 打开二进制文件 |
| 8. | `ios::ate` | 打开文件时文件指针移动到文件末尾 |

所有模式的简要描述如下：

- **1. `ios::trunc`** 如果文件已存在，其内容将被丢弃。如果指定了 `ios::out`，并且未指定 `ios::ate`、`ios::app` 和 `ios::in`，则隐含此模式。

- **2. `ios::noreplace`** 如果文件已存在，函数将失败。此模式会自动为写入打开文件，如果文件不存在。

- **3. `ios::binary`** 以二进制模式打开文件（默认在文本模式）。

- **4. `ios::in`** 文件被打开以进行输入。如果文件存在，原文件将不会被截断。

- **5. `ios::ate`** 函数执行到文件末尾的 seek。当第一个新字节写入文件时，它会被追加到末尾，但当后续字节写入时，它们会被写入当前位置，即文件中的任何位置。

- **6. `ios::app`** 函数执行到文件末尾的 seek。当新字节写入文件时，它们始终被追加到末尾，即使使用 `ostream::seekp` 函数移动了位置。

- **7. `ios::nocreate`** 如果文件尚不存在，函数将失败。

文件可以以一种以上的模式打开。可以使用二进制 OR 运算符（|）组合多个模式，如：

```cpp
file.open("demo.txt", ios::in | ios::out | ios::binary);
```

```cpp
/* PROG 12.6 READING AND WRITING THE SAME FILE IN ONE PROGRAM VER 1*/

#include <iostream.h>
#include <fstream.h>

void main()
{
    fstream rw;
    rw.open("demo1.txt", ios::out);
    char str[50];

    cout << "ENTER A STRING" << endl;
    cin.getline(str, 50);

    rw << str << endl;

    rw.close();

    rw.open("demo1.txt", ios::in);
    rw.getline(str, 50);
    cout << "STRING READ FROM FILE" << endl;
    cout << str << endl;

    rw.close();
}
```

**输出：**

ENTER A STRING
Hello pandey
STRING READ FROM FILE
Hello pandey

**说明：** 使用 `fstream` 类的对象，我们可以使用 `open` 函数以读写两种模式打开文件。最初文件以写模式打开，如：

```cpp
rw.open("demo1.txt", ios::out);
```

第二个参数是文件打开标志。`ios` 是一个类，`out` 是该类的属性。合在一起写成 `ios::out`，表示我们以写模式打开文件 `demo1.txt`。如果文件之前不存在，则会创建它。如果已创建，则所有内容将被清除。字符串从标准输入流获取并写入文件，如 `rw << str << endl;` 然后通过调用 `close` 方法关闭文件，如：

```cpp
rw.close();
```

文件关闭会清除与文件 `demo1.txt` 相关的所有缓冲区并解除文件 `demo1.txt` 与 `fstream` 对象 `rw` 的链接。文件关闭是必须的，因为随着字符写入文件，指针会进入文件，因此在将字符串 `str` 输入文件后，指针将向前推进 `sizeof(str)` 字节。为了使指针回到文件开头并重新以读取模式打开文件，必须关闭文件。

要读取我们刚刚输入的文件内容，我们再次打开文件。但这次使用标志 `ios::in` 以读取模式打开。此标志以读取模式打开文件 `demo1.txt`。我们通过编写以下内容从文件中读取字符串：

```cpp
rw.getline(str, 50);
```

它从 `rw` 指向的文件中读取字符串并将字符串存储在 `str` 中。读取的字符串使用标准输出流 `cout` 显示回屏幕。

```cpp
/* PROG 12.7 READING AND WRITING THE SAME FILE IN ONE PROGRAM VER 2 */

#include <iostream.h>
#include <fstream.h>
#include <conio.h>

void main()
{
    fstream rw;
    rw.open("demo1.txt", ios::out | ios::in);
    char str[50];
    clrscr();
    cout << "Enter a string" << endl;
    cin.getline(str, 50);
    rw << str << endl;
    rw.seekg(0, ios::beg);
    rw.getline(str, 50);
    cout << "String read from file" << endl;
    cout << str << endl;
    rw.close();
}
```

**输出：**

Enter a string
MPSTME, NMIMS UNIVERSITY MUMBAI
String read from file
MPSTME, NMIMS UNIVERSITY MUMBAI

![](img/ad5299318df8d4d7c6df5eaa86590ea3_591_0.png)

**图 12.1。** *程序 12.7 的输出屏幕*

**说明：** 我们可以通过使用二进制 OR 符号（`|`）将标志 OR 起来，以一种以上的模式打开文件。语句写为：

```cpp
rw.open("demo1.txt", ios::out | ios::in);
```

![](img/ad5299318df8d4d7c6df5eaa86590ea3_593_0.png)

**图 12.2。** *程序 12.8 的输出屏幕。*

**说明：** 程序很简单。我们从键盘输入手机详细信息，写入文件并关闭文件。我们以读取模式打开文件并从文件中读取手机详细信息，然后显示在屏幕上。

## 12.5 检查文件末尾

当文件被打开以进行读取时，只要文件保持打开并且未遇到文件末尾，就能从文件中读取数据。文件末尾可以通过两种方式检查：

- **（A）** 在第一种方法中，文件流对象可以在 while 循环中写为：

```
while (filestr)
{
    read from file pointer by file str;
    process data;
}
```

只要我们正在读取，`filestr` 就返回非零值。一旦遇到文件末尾，`filestr` 返回零并且 while 循环终止。

- **（B）** 第二种方法是最常用的，使用 `eof()` 函数检查文件末尾。`eof()` 函数只要文件中有数据，即只要未到达文件末尾，就返回零。一旦到达文件末尾，`eof()` 函数返回非零值。它可以与 while 循环一起使用，如：

```
while(filestr.eof() == 0)    or    while(file.eof())
{
    read from file pointer by filestr;
    process data;
}
```

