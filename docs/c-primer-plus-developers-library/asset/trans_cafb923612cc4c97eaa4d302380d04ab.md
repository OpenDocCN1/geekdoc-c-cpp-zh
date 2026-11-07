
## 简单的文件 I/O

假设你希望程序写入文件。必须完成以下步骤：

- 1. 创建一个 `ofstream` 对象来管理输出流。
- 2. 将该对象与特定文件关联。
- 3. 像使用 `cout` 那样使用该对象；唯一区别是输出发送到文件而不是屏幕。

为此，首先包含 `fstream` 头文件。对于大多数（但并非所有）实现，包含该文件会自动包含 `iostream` 文件，因此你可能不必显式包含 `iostream`。然后声明一个 `ofstream` 对象：

```
ofstream fout;        // create an ofstream object named fout
```

该对象的名称可以是任何有效的 C++ 名称，例如 `fout`、`outFile`、`cgate` 或 `didi`。接下来，必须将该对象与特定文件关联。可以使用 `open()` 方法完成关联。例如，假设你想打开 `jar.txt` 文件用于输出，可以这样做：

```
fout.open("jar.txt");   // associate fout with jar.txt
```

可以使用不同的构造函数将这两个步骤（创建对象和关联文件）合并为一条语句：

```
ofstream fout("jar.txt");  // create fout object, associate it with jar.txt
```

做到这一步后，就可以像使用 `cout` 那样使用 `fout`（或你选择的任何名称）。例如，如果想把 Dull Data 这几个词写入文件，可以这样做：

```
fout << "Dull Data";
```

确实，由于 `ostream` 是 `ofstream` 类的基类，你可以使用所有 `ostream` 方法，包括各种插入运算符定义以及格式化方法和操纵器。`ofstream` 类使用缓冲输出，因此程序在创建诸如 `fout` 之类的 `ofstream` 对象时会为输出缓冲区分配空间。如果创建两个 `ofstream` 对象，程序会创建两个缓冲区，每个对象一个。诸如 `fout` 之类的 `ofstream` 对象会从程序逐字节收集输出；然后，当缓冲区填满时，它会将缓冲区内容整体传输到目标文件。由于磁盘驱动器设计为以更大的块传输数据，而不是逐字节传输，因此缓冲方法大大加快了数据从程序到文件的传输速率。

以这种方式打开文件用于输出时，如果不存在该名称的文件，则会创建一个新文件。如果在打开文件用于输出之前已存在同名文件，则打开操作会截断该文件，使输出从干净的文件开始。本章后面你将看到如何打开现有文件并保留其内容。

> **注意**
>
> 以默认模式打开文件用于输出会自动将文件截断为零大小，实际上会丢弃先前的内容。

读取文件的要求与写入文件非常相似：

- 1. 创建一个 `ifstream` 对象来管理输入流。
- 2. 将该对象与特定文件关联。
- 3. 像使用 `cin` 那样使用该对象。

读取文件的步骤与写入文件相似。当然，首先包含 `fstream` 头文件。然后声明一个 `ifstream` 对象并将其与文件名关联。可以用两条语句或一条语句完成：

```
// two statements
ifstream fin;                // create ifstream object called fin
fin.open("jellyjar.txt");    // open jellyjar.txt for reading
// one statement
ifstream fis("jamjar.txt");  // create fis and associate with jamjar.txt
```

然后就可以像使用 `cin` 那样使用 `fin` 或 `fis`。例如，可以使用以下代码：

```
char ch;
fin >> ch;                  // read a character from the jellyjar.txt file
char buf[80];
fin >> buf;                 // read a word from the file
fin.getline(buf, 80);       // read a line from the file
string line;
getline(fin, line);         // read from a file to a string object
```

输入与输出一样是缓冲的，因此创建诸如 `fin` 之类的 `ifstream` 对象会创建一个输入缓冲区，由 `fin` 对象管理。与输出一样，缓冲传输数据比逐字节传输快得多。

当输入和输出流对象失效时（例如程序终止时），与文件的连接会自动关闭。也可以使用 `close()` 方法显式关闭与文件的连接：

```
fout.close();       // close output connection to file
fin.close();        // close input connection to file
```

关闭这样的连接并不会消除流；它只是将流与文件断开。不过，流管理机制仍然保留。例如，`fin` 对象仍然存在，连同它管理的输入缓冲区。稍后你会看到，可以将该流重新连接到同一文件或另一个文件。

让我们看一个简短的示例。代码清单 17.16 中的程序请求输入一个文件名。它创建一个具有该名称的文件，向其中写入一些信息，然后关闭该文件。关闭文件会刷新缓冲区，确保文件已更新。然后程序打开同一个文件进行读取并显示其内容。注意，程序使用 `fin` 和 `fout` 的方式与你使用 `cin` 和 `cout` 的方式相同。此外，程序将文件名读入一个 `string` 对象，然后使用 `c_str()` 方法为 `ofstream` 和 `ifstream` 构造函数提供 C 风格字符串参数。

### 代码清单 17.16 fileio.cpp

```cpp
// fileio.cpp -- saving to a file
#include <iostream> // not needed for many systems
#include <fstream>
#include <string>

int main()
{
    using namespace std;
    string filename;

    cout << "Enter name for new file: ";
    cin >> filename;

// create output stream object for new file and call it fout
    ofstream fout(filename.c_str());

    fout << "For your eyes only!\n";        // write to file
    cout << "Enter your secret number: ";   // write to screen
    float secret;
    cin >> secret;
    fout << "Your secret number is " << secret << endl;
    fout.close();       // close file

// create input stream object for new file and call it fin
    ifstream fin(filename.c_str());
    cout << "Here are the contents of " << filename << ":\n";
    char ch;
    while (fin.get(ch))     // read character from file and
        cout << ch;         // write it to screen
    cout << "Done\n";
    fin.close();

    return 0;
}
```

下面是代码清单 17.16 中程序的一次示例运行：

```
Enter name for new file: pythag
Enter your secret number: 3.14159
Here are the contents of pythag:
For your eyes only!
Your secret number is 3.14159
Done
```

如果检查包含该程序的目录，你应该会找到一个名为 pythag 的文件，任何文本编辑器都应显示与程序输出相同的内容。（保密到此为止。）

### 流检查与 is_open()

C++ 文件流类从 `ios_base` 类继承一个流状态成员。如前所述，该成员存储反映流状态的信息：一切正常、已到达文件末尾、I/O 操作失败等。如果一切正常，流状态为零（没消息就是好消息）。其他各种状态通过将特定位设置为 1 来记录。文件流类还继承 `ios_base` 中报告流状态的方法，这些方法汇总在表 17.4 中。可以检查流状态来判断最近的流操作是成功还是失败。对于文件流，这包括检查尝试打开文件是否成功。例如，尝试打开不存在的文件用于输入会设置 `failbit`。因此可以这样检查：

```
fin.open(argv[1]);
if (fin.fail())  // open attempt failed
{
    ...
}
```

或者，由于 `ifstream` 对象和 `istream` 对象一样，在需要 `bool` 类型的地方会转换为 `bool` 类型，你可以使用以下写法：

```
fin.open(argv[1]);
if (!fin)  // open attempt failed
{
    ...
}
```

不过，较新的 C++ 实现提供了一种更好的方法来检查文件是否已打开——`is_open()` 方法：

```
if (!fin.is_open())  // open attempt failed
{
    ...
}
```

这种方法更好的原因是，它会检测其他形式遗漏的一些微妙问题，如下面的“注意”所述。
