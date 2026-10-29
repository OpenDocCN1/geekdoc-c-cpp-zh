

# 程序 9.7

```
#include <iostream>
#include <fstream>
#include <string>
#include <cstdlib>
using namespace std;

int main()
{
    string filename = "test.dat";
    char ch;
    long offset, last;

    ifstream inFile(filename.c_str());

    if (inFile.fail())  // check for successful open
    {
        cout << "\nThe file was not successfully opened"
             << "\n Please check that the file currently exists"
             << endl;
        exit(1);
    }

    inFile.seekg(0L, ios::end);   // move to the end of the file
    last = inFile.tellg();        // save the offset of the last character

    for(offset = 1L; offset <= last; offset++)
    {
        inFile.seekg(-offset, ios::end);
        ch = inFile.get();
        cout << ch << " : ";
    }

    inFile.close();

    cout << endl;

    return 0;
}
```

假设 test.dat 文件包含以下字符：

The grade was 92.5

程序 9.7 的输出如下：

```
5 : . : 2 : 9 :   : s : a : w :   : e : d : a : r : g :   : e : h : T :
```

程序 9.7 最初移动到文件中的最后一个字符。此字符的偏移量，即 EOF 字符，被保存在变量 last 中。因为 tellg() 返回一个长整数，所以 last 已被声明为长整数。

从文件末尾开始，seekg() 用于定位要读取的下一个字符，相对于文件末尾引用。随着每个字符的读取，它会被显示出来，并且偏移量会被调整以访问下一个字符。使用的第一个偏移量是 -1，它表示紧邻 EOF 标记之前的字符。

## 练习 9.3

+   1. （练习）a. 创建一个名为 test.dat 的文件，其中包含程序 9.7 中使用的 test.dat 文件中的数据。 （你可以使用文本编辑器或从本书网站复制 test.dat 文件。）
+      b. 在你的计算机上输入并运行程序 9.7。
+   2. （修改）重写程序 9.7，使 for 循环中使用的 seekg() 方法的原点为文件的开头而不是末尾。
+   3. （修改）修改程序 9.7，如果 seekg() 尝试引用文件末尾之外的某个位置，则显示错误消息。
+   4. （练习）编写一个程序，读取并显示名为 test.dat 的文件中每隔一个字符。
+   5. （练习）使用 seek() 和 tell() 方法，编写一个名为 fileChars() 的函数，该函数返回文件中的总字符数。
+   6. （练习）a. 编写一个名为 readBytes() 的函数，该函数从文件中的任意位置读取并显示 n 个字符。 该函数应接受三个参数：文件对象名、要读取的第一个字符的偏移量以及要读取的字符数。 （注意：readBytes() 的原型应为 void readBytes(fstreams, long, int)。）
+      b. 修改练习 6a 中编写的 readBytes() 函数，将读取的字符存储到字符串或数组中。 该函数应接受存储地址作为第四个参数。

## 9.4 文件流作为函数参数

文件流对象可以用作函数参数。唯一的要求是函数的形参必须是正确的流的引用（参见第 6.3 节）：ifstream& 或 ofstream&。例如，在程序 9.8 中，ofstream 对象名为 outfile 在 main() 中打开，并且此流对象被传递给 inOut() 函数。 inOut() 的函数原型和头声明形参为 ostream 对象类型的引用。 inOut() 函数随后用于将五行用户输入的文本写入文件。

# 程序 9.8

```
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int main()
{
    string fname = "list.dat";  // here is the file you are working with
    void inOut(ofstream&);       // function prototype
    ofstream outFile;

    outFile.open(fname.c_str());

    if (outFile.fail())    // check for a successful open
    {
        cout << "\nThe output file " << fname << " was not successfully opened" << endl;
        exit(1);
    }

    inOut(outFile);  // call the function

    return 0;
}

void inOut(ofstream& fileOut)
{
    const int NUMLINES = 5;  // number of lines of text
    string line;
    int count;

    cout << "Please enter five lines of text:" << endl;
    for (count = 0; count < NUMLINES; count++)
    {
        getline(cin,line);
        fileOut << line << endl;
    }

    cout << "\nThe file has been successfully written." << endl;

    return;
}
```

在 main() 中，文件是一个名为 outFile 的 ostream 对象。此对象被传递给 inOut() 函数并作为形参 fileOut 接受，该形参被声明为 ostream 对象类型的引用。 inOut() 函数随后使用其引用参数 outFile 作为输出文件流名，其方式与 main() 使用 fileOut 流对象的方式相同。程序 9.8 使用第 9.2 节中介绍的 getline() 方法（参见表 9.3）。

程序 9.9 在程序 9.8 的基础上扩展，添加了 getOpen() 函数来执行打开操作。像 inOut() 一样，getOpen() 接受对 ofstream 对象的引用参数。 getOpen() 执行完毕后，此引用被传递给 inOut()，如程序 9.8 中所示。虽然你可能想编写 getOpen() 以返回对 ofstream 的引用，但它不起作用，因为它会导致尝试将返回的引用分配给已存在的引用。

# 程序 9.9

```
#include <iostream>
#include <fstream>
#include <cstdlib>
#include <string>
using namespace std;

int getOpen(ofstream&);  // function prototype - pass a
                         // reference to an fstream
void inOut(ofstream&);   // function prototype - pass a
                         // reference to an fstream

int main()
{
    ofstream outFile;    // filename is an fstream object

    getOpen(outFile);    // open the file
    inOut(outFile);      // write to it

    return 0;
}

int getOpen(ofstream& fileOut)
{
    string name;

    cout << "\nEnter a filename: ";
    getline(cin,name);

    fileOut.open(name.c_str());    // open the file

if (fileOut.fail())    // check for successful open
{
    cout << "Cannot open the file" << endl;
    exit(1);
}
else
    return 1;
}

void inOut(ofstream& fileOut)
{
    const int NUMLINES = 5;  // number of lines
    int count;
    string line;

    cout << "Please enter five lines of text:" << endl;
    for (count = 0; count < NUMLINES; ++count)
    {
        getline(cin,line);
        fileOut << line << endl;
    }
    cout << "\nThe file has been successfully written.";

    return;
}
```

程序 9.9 允许用户从标准输入设备输入文件名，然后打开 ofstream 连接到外部文件。如果输入了现有数据文件的名称，在打开用于输出时文件将被销毁。防止此事故的一个有用技巧在程序 9.2 的阴影代码中显示。

## 练习 9.4

+   1. （练习）一个名为 pFile() 的函数将接收一个文件名作为对 ifstream 对象的引用。传递文件名给 pFile() 需要哪些声明？
+   2. （练习）编写一个名为 fcheck() 的函数来检查文件是否存在。 该函数应接受 ifstream 对象作为形式引用参数。如果文件存在，函数应返回值为 1；否则，函数应返回值为 0。
+   3. （练习）已创建由一组行组成的数据文件。编写一个名为 printLine() 的函数，该函数读取并显示文件的任意一行。例如，函数调用 printLine(ifstream& fName,5); 应显示所传递对象流的第五行。
+   4. （修改）重写程序 9.9 中使用的 getOpen() 函数，以纳入本节中描述的文件检查程序。具体来说，如果输入的文件名存在，应显示适当的<|message|>。用户应有机会输入新的文件名或允许程序覆盖现有文件。使用练习 2 中编写的函数在你的程序中使用。

## 9.5 常见编程错误

与文件相关的常见编程错误如下：

+   1. 在尝试从文件中读取或写入文件之前忘记打开文件。
+   2. 在访问文件时使用文件的外部名称代替内部文件流对象名称。唯一使用数据文件的外部名称的流方法是 open() 方法。 始终，所有本章讨论的流方法必须以流对象名称开头，后跟句点（点运算符）。
+   3. 在未先检查是否已存在同名文件的情况下打开文件进行输出。如果存在且你未检查预先存在的文件名，则文件将被覆盖。
+   4. 不理解文件末尾仅在 EOF 标记已被读取或越过后才被检测到。
+   5. 尝试通过使用字符变量来检测文件末尾的 EOF 标记。用于接受 EOF 的任何变量必须声明为整数变量。 例如，如果 ch 声明为字符变量，则以下表达式会产生无限循环：

```
while ( ch = in.file.peek() ) != EOF
```

此问题发生的原因是字符变量永远无法采用 EOF 代码。 EOF 是一个整数值（通常为 -1），没有字符表示，这确保 EOF 代码不会与文件中的正常数据中遇到的合法字符混淆。为了终止上述表达式创建的循环，变量 ch 必须声明为整数变量。
+   6. 使用整数参数与 seekg() 和 seekp() 函数一起使用。此偏移量必须是长整数常量或变量。传递给这些函数的任何其他值都可能产生不可预测的结果。

## 9.6 章节总结

+   1. 数据文件是存储在外部存储介质中并在共同名称下存储在一起的任何数据集合。
+   2. 数据文件通过使用文件流对象连接到文件流。

