

尽管我们使用了单个程序，但创建了两个文件流对象：outfile（用于将数据写入文件）和 infile（用于从文件读取数据）。请注意，使用像 `outfile.close();` 这样的语句会将 salary 文件与输出流 outfile 断开连接。切记，outfile 对象仍然存在，salary 文件以后可以重新连接到 outfile，也可以连接到任何其他流。在本例中，我们将 salary 文件连接到 infile 流以读取数据。

程序 11.1 使用同一个文件进行数据的写入和读取。首先，它从键盘读取数据并写入文件。写入完成后，文件被关闭。程序再次打开同一个文件，读取已经写入其中的信息，并将其显示在屏幕上。

## 程序 11.1 使用单个文件

```cpp
#include <iostream.h>
#include <fstream.h>

int main()
{
    ofstream outf("ITEM");    // connect ITEM file to outf
    cout << "Enter item name:";
    char name[30];
    cin >> name;    // get name from keyboard and
    outf << name << "\n";    // write to file ITEM
}
```

程序 11.1 的输出如下：

```
Enter item name:CD-ROM
Enter item cost:250

Item name:CD-ROM
Item cost:250
```

> **注意：***当文件仅以写入方式打开时，如果不存在同名文件，则会创建一个新文件。如果同名文件已经存在，其内容将被删除，文件以空文件形式呈现。我们将在后面讨论如何打开现有文件进行更新，同时不丢失其原始内容。*

## 使用 open() 打开文件

如前所述，open() 函数可用于打开使用同一个流对象的多个文件。例如，我们可能需要按顺序处理一组文件。在这种情况下，我们可以创建一个流对象，并依次使用它打开每个文件。具体做法如下：

```
file-stream-class stream-object;
stream-object.open ("filename");
```

示例：

```
ofstream outfile;              // Create stream (for output)
outfile.open("DATA1");         // Connect stream to DATA1
....
....
outfile.close();               // Disconnect stream from DATA1
outfile.open("DATA2");         // Connect stream to DATA2
....
....
outfile.close();               // Disconnect stream from DATA2
....
....
```

上面的程序段按顺序打开两个文件用于写入数据。注意，在打开第二个文件之前必须先关闭第一个文件。这是必要的，因为一个流同时只能连接一个文件。参见程序 11.2 和图 11.1。

## 程序 11.2 使用多个文件

[第 480 页]

```cpp
// Creating files with open() function

#include <iostream.h>
#include <fstream.h>

int main()
{
    ofstream fout;                 // create output stream
    fout.open("country");         // connect "country" to it

    fout << "United States of American";
    fout << "United Kingdom\n";
    fout << "South Korea\n";

    fout.close();                  // disconnect "country" and

    fout.open("capital");          // connect "capital"

    fout << "Washington\n";
    fout << "London\n";
    fout << "Seoul\n";

    fout.close();                  // disconnect "capital"

    // Reading the files
    const int N = 80;              // size of line
    char line[N];

    ifstream fin;                  // create input stream
    fin.open("country");           // connect "country" to it

    cout << "contents of country file\n";

    while(fin)                     // check end-of-file
    {
        fin.getline(line, N);      // read a line
    }
```

程序 11.3 的输出如下：

```
Capital of United States of America

Washington

Capital of United Kingdom

London
```

[第 481 页]

<!-- 无内容 -->

[第 482 页]

<!-- 无内容 -->

[第 483 页]

```
{<br>
const int SIZE = 80;<br>
char line[SIZE];<br>
<br>
ifstream fin1, fin2; // create two input streams<br>
fin1.open("country");<br>
fin2.open("capital");<br>
<br>
for(int i=1; i<=10; i++)<br>
{<br>
if(fin1.eof() != 0)<br>
{<br>
cout << "Exit from country \n";<br>
exit(1);<br>
}<br>
<br>
fin1.getline(line, SIZE);<br>
cout << "Capital of "<< line ;<br>
if(fin2.eof() != 0)<br>
{<br>
cout << "Exit from capital\n";<br>
exit(1);<br>
}<br>
<br>
fin2.getline(line,SIZE);<br>
cout << line << "\n";<br>
}<br>
return 0;<br>
}
```

[第 484 页]

<!-- 无内容 -->

[第 485 页]

第二个参数用于指定文件模式。带两个参数的 open() 函数的一般形式是：

> stream-object.open("filename", mode);

第二个参数 mode（称为文件模式参数）指定打开文件的目的。那么，在前面的示例中，我们在没有提供第二个参数的情况下是如何打开文件的呢？

这些类成员函数的原型为第二个参数提供了默认值，因此在没有实际值的情况下会使用默认值。默认值如下：

> `ios::in` 用于 ifstream 函数，表示只读打开；`ios::out` 用于 ofstream 函数，表示只写打开。

文件模式参数可以取 ios 类中定义的一个（或多个）此类常量。表 11.2 列出了文件模式参数及其含义。

| *参数* | *含义* |
|------|------|
| `ios::app` | 追加到文件末尾 |
| `ios::ate` | 打开时定位到文件末尾 |
| `ios::binary` | 二进制文件 |
| `ios::in` | 打开文件，仅用于读取 |
| `ios::nocreate` | 如果文件不存在，则打开失败 |
| `ios::noreplace` | 如果文件已存在，则打开失败 |
| `ios::out` | 打开文件，仅用于写入 |
| `ios::trunc` | 如果文件存在，则删除其内容 |

+   1. 以 `ios::out` 模式打开文件时，默认也会以 `ios::trunc` 模式打开。
+   2. 打开文件时，`ios::app` 和 `ios::ate` 都会将位置定位到文件末尾。两者的区别在于，`ios::app` 只允许在文件末尾添加数据，而 `ios::ate` 模式允许在文件中的任意位置添加或修改已有数据。在这两种情况下，如果指定名称的文件不存在，都会创建该文件。
+   3. 参数 `ios::app` 只能用于能够输出的文件。
+   4. 使用 `ifstream` 创建流意味着输入，使用 `ofstream` 创建流意味着输出。因此，在这些情况下不必提供模式参数。
+   5. `fstream` 类默认不提供模式，因此在使用 `fstream` 类对象时，我们必须显式提供模式。
+   6. 模式可以使用按位 OR 运算符（符号 `|`）组合两个或多个参数，如下所示：
+   
+      `fout.open(“data”, ios::app | ios::nocreate)`
+   
+      这将以追加模式打开文件，但如果文件不存在，则打开失败。

## 11.6 文件指针及其操作

每个文件都有两个关联的指针，称为*文件指针*。其中一个称为输入指针（*或 get 指针*），另一个称为输出指针（*或 put 指针*）。在读取或写入时，我们可以使用这些指针在文件中移动。输入指针用于读取给定文件位置的内容，输出指针用于写入给定文件位置的内容。每次执行输入或输出操作时，相应的指针都会自动前进。

