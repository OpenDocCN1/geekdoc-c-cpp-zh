

```cpp
inFile.open(filename.c_str());  // open the file

if (inFile.fail())  // check for successful open
{
    cout << "\nThe file named " << filename
         << " was not successfully opened"
         << "\n Please check that the file currently exists."
         << endl;
    exit(1);
}

cout << "\nThe file has been successfully opened for reading.\n";

return 0;
}
```

在程序 9.3a 中，声明了一个 string 对象，并用文件名 filename 进行初始化。¹ 这个名称被放在 main() 函数开头，便于识别和修改文件。当使用 string 对象而不是字符串字面量时，在调用 open() 方法时对象名不需要用双引号括起来。但是，由于 open() 要求使用 C-字符串（string 类不使用 C-字符串），因此必须在 open() 调用中将 string 对象转换为 C-字符串，这是通过表达式 filename.c_str() 中的 c_str() 方法完成的。

最后，在 fail() 方法中，通过将 string 对象的名称插入到 cout 输出流中来显示文件的外部名称。本书中均以这种方式标识文件的外部名称。

string 对象的另一个有用作用是允许用户在程序运行时输入文件名。例如，代码

```cpp
string filename;

cout << "Please enter the name of the file you wish to open: ";
cin >> filename;
```

允许用户在运行时输入文件的外部名称。这段代码的唯一限制是，用户输入字符串值时不能加上双引号，并且输入的字符串值不能包含任何空格。之所以不能包含空格，是因为使用 cin 时，编译器遇到空格就会终止字符串。程序 9.3b 在完整程序的上下文中使用了这段代码。

> ¹如果文件位于 C 盘的 datafiles 文件夹中，指定完整路径名则需要如下语句：
>
> ```cpp
> string filename = "C:\\datafiles\\prices.dat";
> ```

## 程序 9.3b

```cpp
#include <iostream>
#include <fstream>
#include <cstdlib>  // needed for exit()
#include <string>  // needed for the string class
using namespace std;

int main()
{
    string filename; // declare a string object with no initialization
    ifstream inFile;

    cout << "Please enter the name of the file you wish to open: ";
    cin >> filename;

    inFile.open(filename.c_str());  // open the file
    if (inFile.fail())  // check for successful open
    {
        cout << "\nThe file named " << filename
             << " was not successfully opened"
             << "\n Please check that the file currently exists."
             << endl;
        exit(1);
    }
    cout << "\nThe file has been successfully opened for reading.\n";

    return 0;
}
```

以下是程序 9.3b 的示例输出：

```
Please enter the name of the file you wish to open: foobar

The file named foobar was not successfully opened
Please check that the file currently exists.
```

## 知识点

### 标识文件名称和位置的方法

在程序开发过程中，测试文件通常放在与程序相同的目录或文件夹中。因此，诸如 inFile.open("exper.dat") 之类的方法调用不会给操作系统带来任何问题。然而，在生产系统中，数据文件位于一个文件夹而程序文件位于另一个文件夹的情况并不少见。因此，在打开任何文件时包含完整路径名始终是一个好主意。

例如，如果 exper.dat 文件位于 C:\test\files 目录中，则 open() 调用应包含完整路径名：inFile.open("C:\\test\\files\\exper.dat")。然后，无论程序从哪里运行，操作系统都知道在哪里找到该文件。注意必须使用双反斜杠。

另一个重要的约定是，将所有文件名列在程序顶部，而不是将名称嵌入到代码深处。你可以通过将每个文件名声明为 string 对象（或一维字符数组）轻松做到这一点。例如，将以下语句放在程序文件顶部，可以清楚地列出文件名及其位置：

```
string filename = "c:\\test\\files\\exper.dat";
```

如果要测试其他文件，只需简单更改此易查找语句中的字符串字面量即可。请记住，使用 string 类需要在程序中添加 #include <string> 指令。

### 关闭文件

文件通过使用 close() 方法关闭。此方法断开文件外部名称与文件流对象之间的连接，该文件流对象可用于另一个文件。请查看以下语句，它关闭了 inFile 流与其当前文件的连接：

```
inFile.close();
```

如所示，close() 方法不带参数。

由于所有计算机对一次可打开的最大文件数都有限制，因此关闭不再需要的文件是明智之举。正常程序执行结束时存在的任何打开的文件都会由操作系统自动关闭。

## 知识点

### 使用 fstream 对象

在使用 ifstream 和 ofstream 对象时，输入或输出模式由对象指示。因此，ifstream 对象必须用于输入，而 ofstream 对象必须用于输出。创建文件流的另一种方法是使用 fstream 对象，它可以用于输入或输出，但这种方法需要显式指定模式。使用以下语法声明 fstream 对象：

```
fstream objectName;
```

使用 fstream 类的 open() 方法时，需要两个参数：文件的外部名称和模式指示符。以下是允许的模式指示符；除了前两个之外，它们也可以在打开 ifstream 和 ofstream 对象时使用：

| 指示符 | 说明 |
|---|---|
| ios::in | 以输入模式打开文本文件（不用于 ifstream 对象） |
| ios::out | 以输出模式打开文本文件（不用于 ofstream 对象） |
| ios::app | 以追加模式打开文本文件 |
| ios::ate | 转到打开的文件的末尾 |
| ios::binary | 以输入模式打开二进制文件（默认为文本文件） |
| ios::trunc | 如果文件存在则删除其内容 |
| ios::nocreate | 如果文件不存在，打开失败 |
| ios::noreplace | 如果文件存在，则打开用于输出的操作失败 |

与 ofstream 对象一样，处于输出模式的 fstream 对象会创建新文件并使该文件可用于写入。如果存在与打开用于输出的文件同名的文件，则旧文件会被删除。例如，以下语句将 file1 声明为 fstream 类型的对象：

```
fstream file1;
```

以下语句尝试打开文本文件 prices.dat 以进行输出：

```
file1.open("prices.dat",ios::out);
```

该文件打开后，程序使用内部对象名 file1 访问该文件，计算机则以外部名称 prices.dat 保存该文件。

以追加模式打开的 fstream 文件对象意味着现有文件可用于将数据添加到文件末尾。如果打开用于追加的文件不存在，则会创建一个指定名称的新文件，并使其可用于接收程序的输出。例如，以下语句将 file1 声明为 fstream 对象，并尝试打开名为 prices.dat 的文本文件，使其可用于将数据添加到文件末尾：

```
file1.open("prices.dat",ios::app);
```

## 知识点

### 使用 fstream 对象（续）

最后，以输入模式打开的 fstream 对象意味着已连接一个现有的外部文件，并且其数据可作为输入。例如，以下语句将 file1 声明为 fstream 类型，并尝试打开名为 prices.dat 的文本文件以进行输入：

```
file1.open("prices.dat", ios::in);
```

模式指示符可以通过按位或运算符 | 组合（参见附录 C，在线提供）。例如，以下语句将 file1 流（可以是 fstream 或 ifstream 对象）作为输入二进制流打开：

```
file1.open("prices.dat", ios::in | ios::binary)
```

如果对 ifstream 对象省略作为第二个参数的模式指示符，则默认以文本输入文件方式打开流；如果对 ofstream 对象省略模式指示符，则默认以文本输出文件方式打开流。

## 练习 9.1

- 1. （练习）编写声明和打开语句，将以下外部文件名与其对应的内部文件名相连接。所有文件均基于文本。

| 外部文件名 | 内部文件名 | 模式 |
|---|---|---|
| coba.mem | memo | 输出 |
| book.let | letter | 输出 |
| coupons.bnd | coups | 追加 |
| yield.bnd | yield | 追加 |
| prices.dat | priFile | 输入 |
| rates.dat | rates | 输入 |

- 2. （练习）a. 编写一组两条语句，将以下对象声明为 ifstream 对象，然后将其作为文本输入文件打开：inData.txt、prices.txt、coupons.dat 和 exper.dat。
- b. 使用一条语句重写练习 2a 的两条语句。

- 3. （练习）a. 编写一组两条语句，将以下对象声明为 ofstream 对象，然后将其作为文本输出文件打开：outDate.txt、rates.txt、distance.txt 和 file2.txt。
- b. 使用一条语句重写练习 3a 的两条语句。

