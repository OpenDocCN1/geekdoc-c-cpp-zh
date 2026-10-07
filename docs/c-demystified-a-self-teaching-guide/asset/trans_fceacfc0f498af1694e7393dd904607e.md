
```cpp
int main ()
{
    string data;
    ofstream outfile;
    outfile.open("students.dat");
    cout << "Writing to the file" << endl;
    cout << "====================" << endl;
    cout << "Enter class name: ";
    getline(cin, data);
    outfile << data << endl;
    cout << "Enter number of students: ";
    cin >> data;
    cin.ignore();
    outfile << data << endl;
    outfile.close();
    ifstream infile;
    cout << "Reading from the file" << endl;
    cout << "====================" << endl;
    infile.open("students.dat");
    getline(infile, data);
    cout << data << endl;
    getline(infile, data);
    cout << data << endl;
    infile.close();
    return 0;
}
```

如下面的示例输入和输出结果，第一次读取现在会读取文件的整个第一行，即使该行包含空格：

Writing to the file
====================
Enter class name: Programming Demystified
Enter number of students: 32
Reading from the file
====================
Programming Demystified
32

# 循环遍历文件

在之前的程序中，恰好进行了两次读取尝试，因为我们知道文件中有两行数据，不多不少。然而，我们可能不知道需要读取的片段数量。我们想要的只是一直读取文件，直到到达它的末尾。

`ifstream` 对象有一个 `end` 函数，它是 "end of file"文件结束）的缩写。该函数不接受任何参数，如果已到达文件末尾则返回 `true`，否则返回 `false`。

然而，`end` 函数在检测文件末尾时对于文本文件并不像对于二进制文件那样可靠。如果文件的最后一个项目后面紧跟着一个或多个空白字符，`end` 函数的返回值可能无法准确反映是否到达了文件结束。这在二进制文件中不是问题，因为它们不包含空白字符。

更好的选择是 `fail` 成员函数，它在前面的章节“检查文件是否已打开”中讨论过。下面的代码段展示了如何使用 `fail` 成员函数读取文件直到到达末尾：

```cpp
ifstream infile;
infile.open("students.dat");
infile >> data;
while(!infile) {
    infile >> data;
    cout << data;
}
infile.close();
```

前面的代码段包含 `infile >> data` 语句，一个在循环开始前，另一个在循环内部。这是因为只有在进行读取尝试之后，才能检测到文件末尾。如果文件是空的，循环前的 `count << data`（此处应为 infile >> data）语句将被省略，且该语句将在尝试检测是否到达文件末尾之前执行。

- **注意**：可以使用 `while` 循环代替 `if` 循环。这样可以省去在结束循环前检查文件的需要，但会增加在循环末尾检查（使用 `if` 语句）循环是否已到达文件末尾的要求。这是 `while` 循环和 `do` 循环之间常见的权衡。

修改之前的程序，代码现在将：

```cpp
#include <fstream>
#include <iostream>
#include <string>
using namespace std;

int main() {
    string data;
    ofstream outfile;
    outfile.open("students.dat");
    cout << "Writing to the file" << endl;
    cout << "--------------------------------" << endl;
    cout << "Enter class name: ";
    getline(cin, data);
    outfile << data << endl;
    cout << "Enter number of students: ";
    cin >> data;
    cin.ignore();
    outfile << data << endl;
    outfile.close();

    ifstream infile;
    cout << "Reading from the file" << endl;
    cout << "--------------------------------" << endl;
    infile.open("students.dat");
    getline(infile, data);
    // (此处根据原文逻辑重复部分已处理)
    // ... (后续逻辑省略)
    return 0;
}
```
*(注：由于提供的待翻译文本后期存在大量重复和截断的片段，译文已根据原文逻辑对可读部分进行了翻译和整理，并保留了代码结构。)*
