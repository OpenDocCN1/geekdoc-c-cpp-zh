

## 显示 12.2 向文件追加

```
1 //Appends data to the end of the file alldata.txt.
2 #include <fstream>
3 #include <iostream>
4 using std::ofstream;
5 using std::cout;
6 using std::ios;
7 int main( )
8 {
9     cout << "Opening data.txt for appending.\n";
10    ofstream fout;
11    fout.open("data.txt", ios::app);
12
13    fout << "5 6 pick up sticks.\n"
14        << "7 8 ain't C++ great!\n";
15
16    fout.close( );
17    cout << "End of appending to file.\n";
18
19    return 0;
20 }
```

示例对话

# Data.txt
(程序运行前)

1 2 buckle my shoe.
3 4 shut the door.

# Data.txt
(程序运行后)

1 2 buckle my shoe.
3 4 shut the door.
5 6 pick up sticks.
7 8 ain't C++ great!

# 屏幕输出

Opening data.txt for appending.
End of appending to file

## 向文件追加

如果你想将数据追加到文件中，使其位于文件现有内容之后，请按如下方式打开文件。

## 语法

```
Output_Stream.open(File_Name, ios::app);
```

## 示例

```
ofstream outStream;
outStream.open("important.txt", ios::app);
```

## 提示：打开文件的另一种语法

类 ifstream 和 ofstream 各自都有构造函数，允许你指定文件名，有时还可指定其他参数来打开文件。几个示例将使语法变得清晰。

以下两个语句

```
ifstream inStream;
inStream.open("infile.txt");
```

可以用以下等价行替换：

```
ifstream inStream("infile.txt");
```

以下两个语句

```
ofstream outStream;
outStream.open("outfile.txt");
```

可以用以下等价行替换：

```
ofstream outStream("outfile.txt");
```

作为最后一个示例，以下两行

```
ofstream outStream;
outStream.open("important.txt", ios::app);
```

等价于以下内容：

```
ofstream outStream("important.txt", ios::app);
```

## 提示：检查文件是否成功打开

open 的调用可能因多种原因而失败。例如，如果你尝试打开一个输入文件，但不存在你指定的外部名称的文件，则 open 的调用将失败。另一个例子是，尝试打开输出文件可能会失败，因为文件存在，而你的程序（即你的账户）对该文件没有写权限。当出现这种情况时，你可能不会收到错误消息，你的程序可能会继续执行一些意想不到的操作。因此，你应该始终在 open 的调用后进行测试，以查看 open 的调用是否成功，如果 open 的调用不成功，则结束程序（或采取其他适当措施）。

你可以使用名为 fail 的成员函数来测试流操作是否失败。类 ifstream 和 ofstream 各自都有名为 fail 的成员函数。fail 函数不带参数并返回一个 bool 值。

你应该在每次 open 调用之后立即调用 fail；如果 open 调用失败，fail 函数将返回 true。例如，如果以下 open 调用失败，则程序将输出错误消息并结束；如果调用成功，fail 函数返回 false，程序将继续。

```
inStream.open("stuff.txt");
if (inStream.fail())
{
  cout << "Input file opening failed.\n";
  exit(1);
}
```

显示 12.3 包含显示 12.1 中的程序重写，加入了检查输入和输出文件是否成功打开的测试。它以与显示 12.1 中的程序完全相同的方式处理文件。特别是，假设文件 infile.txt 存在并且具有显示 12.1 中所示的内容，则显示 12.3 中的程序将创建显示 12.1 中所示的 outfile.txt 文件。然而，如果出现问题并且其中一个 open 调用失败，则显示 12.3 中的程序将结束并向屏幕发送适当的错误消息。例如，如果不存在名为 infile.txt 的文件，则 inStream.open 的调用将失败，程序将结束，并且错误消息将被写入屏幕。请注意，我们使用了 cout 来输出错误消息；这是因为我们希望错误消息输出到屏幕，而不是输出到文件。由于此程序使用 cout 输出到屏幕（以及进行文件 I/O），我们已添加了对头文件 <iostream> 的包含指令。（实际上，当你的程序已包含 #include <fstream> 时，你的程序不需要 #include <iostream>，但包含它不会造成问题，并且它提醒你程序除了文件 I/O 外还使用屏幕输出。）

成员函数 fail

## 文件 I/O 语句摘要

在此示例中，输入来自名为 `infile.txt` 的文件，输出发送到名为 `outfile.txt` 的文件。

- 在你的程序文件中放置以下包含指令：
  
  ```cpp
  #include <fstream>   // For file I/O
  #include <iostream>  // For cout
  #include <cstdlib>   // For exit
  ```

添加以下 using 指令（或类似内容）：

```
using std::ifstream;
using std::ofstream;
using std::cout;
using std::endl; //if endl is used.
```

- 为输入流选择一个流名并将其声明为 `ifstream` 类型的变量。为输出文件选择一个流名并将其声明为 `ofstream` 类型。例如，
  
  ```cpp
  ifstream inStream;
  ofstream outStream;
  ```

- 使用成员函数 `open` 并将外部文件名作为参数，将每个流连接到文件。记得使用成员函数 `fail` 来测试 open 调用是否成功。
  
  ```cpp
  inStream.open("infile.txt");
  if (inStream.fail())
  {
      cout << "Input file opening failed.\n";
      exit(1);
  }
  outStream.open("outfile.txt");
  if (outStream.fail())
  {
      cout << "Output file opening failed.\n";
      exit(1);
  }
  ```

- 使用流 `inStream` 从文件 `infile.txt` 获取输入，就像使用 `cin` 从键盘获取输入一样。例如，
  
  ```cpp
  inStream >> someVariable >> someOtherVariable;
  ```

*(continued)*

## 文件 I/O 语句摘要（续）

- 使用流 outStream 将输出发送到文件 outfile.txt，就像使用 cout 将输出发送到屏幕一样。例如，
  
      outStream << "someVariable = "
      << someVariable << endl;

- 使用 close 函数关闭流：
  
      inStream.close();
      outStream.close();

## 自测练习

- 1. 假设你正在编写一个使用名为 fin 的流的程序，该流将连接到输入文件，以及一个名为 fout 的流，该流将连接到输出文件。你如何声明 fin 和 fout？你需要在程序文件中放置什么包含指令，如果有的话？

- 2. 假设你正在继续编写上一练习中讨论的程序，并且你希望你的程序从文件 stuff1.txt 读取输入并将输出发送到文件 stuff2.txt。你需要在程序中放置什么语句以将流 fin 连接到文件 stuff1.txt 并将流 fout 连接到文件 stuff2.txt？务必包含检查以确保打开成功。

- 3. 假设你仍在编写前面两个练习中讨论的同一程序，并且你已达到不再需要从文件 stuff1.txt 获取输入并且不再需要向文件 stuff2.txt 发送输出的点。你如何关闭这些文件？

- 4. 假设你想更改显示 12.1 中的程序，使其将输出发送到屏幕而不是文件 outfile.txt。（输入仍应来自文件 infile.txt。）你需要对程序做哪些更改？

- 5. 程序员已读取文件中的一半行。程序员必须对文件做什么才能再次读取第一行？

## 字符 I/O

第 9 章描述了使用 cin 从键盘进行字符 I/O 以及使用 cout 向屏幕进行字符 I/O。来自文件的字符 I/O 的工作方式与键盘和屏幕的字符 I/O 相同。只需使用连接到文件的输入流代替 cin，或使用连接到文件的输出流代替 cout。特别是，get、getline、putback、

