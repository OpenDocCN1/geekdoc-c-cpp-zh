

```cpp
cin.get(ch);
if(ch == '$') break;
EntryFile << ch;
```

之后，同一个文件以读模式打开，以便从中读取。下面的语句执行与现在所做的完全相反的过程。

```cpp
DisplayFile >> ch;
cout << ch;
```

在这两行之前的语句，使用了 unsetf()，需要提及。在读取时，get() 会跳过字符前的空白。因此，如果 get() 读取 "...this is testing"，它会跳过前三个空格，然后读取并返回 't'（字符串的第一个字符）。这对于正常情况是正确的，但在本文中不需要跳过空白。因此，需要提供 unsetf(ios::skipws) 来取消通常跳过空白的设置。

## 13.6.7 使用 getline()

getline() 对于读取整行很有用。

甚至可以用 cout 和 cin 与 getline() 一起使用以提供相同的结果。参见程序 13.3。cin 可用的同一个 getline() 也可用于所有 istream 对象。它也适用于 DisplayFile()。

### PROGRAM 13.3 getline() 函数

```cpp
//Getline.cpp
#include <iostream>
#include <cstring>
#include <fstream>
using namespace std;

int main()
{
    char InputLine[80], OutputLine[80];
    ofstream EntryFile("FewLines.dat");
    while(true)
    {
        cin.getline(InputLine, 80);
        if(!strcmp(InputLine, "End")) break;
        EntryFile << InputLine << endl;
    }
    EntryFile.close();

    ifstream DisplayFile("FewLines.dat");
    while(!DisplayFile.eof())
    {
        DisplayFile.getline(OutputLine, 80);
        cout << OutputLine << endl;
    }
    DisplayFile.close();
    return 0;
}
```

```text
Input
Imagination is
more important
```

### How the Program Works

此程序的唯一重要部分涉及使用 getline() 函数。当执行以下语句时，行（最多 80 个字符，如参数中指定，或直到遇到回车）会被读入输入（如果使用 cin 调用 getline()）或从文件中读取（如果使用文件名调用 getline()）。

```cpp
cin.getline(InputLine, 80);
DisplayFile.getline(OutputLine, 80);
```

可以尝试注释掉此程序中的文件生成代码，使用编辑器构造一个文件，并查看程序的输出。程序将像 DOS 类型命令一样工作并显示文件内容。

> 当我们在文件中读取一个字符串时，文件不会将 <CR> 作为输入。因此，按下 <Enter> 键会终止字符串输入，但文件不会包含该 <Enter>。当文件被读回时，我们将无法在不同行中看到不同的输出。

在本节中，我们将重点关注二进制文件。这些文件对于存储信息结构更有用。

二进制文件可以使用构造函数打开。我们迄今为止看到的 ofstream 和 ifstream 的构造函数适用于文本文件。对于二进制文件，需要另一个具有两个参数的构造函数。第一个参数是文件名，第二个是文件模式。查看以下语句，它们是两种方法的示例。

```cpp
// Using open methods
ofstream MCA_StudyFile_Out;
MCA_StudyFile_Out.open("MCA.dat", ios::out | ios::binary | ios::trunc);
// Using constructor
ifstream MCA_StudyFile_In("MCA.dat", ios::in | ios::binary);
```

第一个示例使用 open 方法，第二个示例使用构造函数。两种打开文件的方式之间没有显著区别。第一种方法使用两个语句而不是一个，并且需要比第二种方法多一点的输入才能达到相同的结果。因此，程序员通常使用第二种使用构造函数的 方法。

也可以通过编写以下任一语句来实现相同效果：

```cpp
ofstream MCA_StudyFile_Out("MCA.dat", ios::out | ios::binary | ios::trunc);
ifstream MCA_StudyFile_In;
MCA_StudFile_In.open("MCA.dat", ios::in | ios::binary);
```

> open 函数也可以与文件一起使用以打开文件。如果我们需要使用不同模式打开同一个文件，open() 很有用。

文件读写操作是使用对象完成的，而不是对象的元素。

构造函数调用和 open 函数产生类似的效果。只有在文件已经打开并且需要以新模式重新打开文件时，才可能键入 close() 然后使用 .open 方法以不同模式打开同一个文件。请注意，在第二个参数中使用管道 ( | ) 来添加多个模式。

## 13.7.2 从二进制文件读取和写入

ifstream 和 ofstream 对象的两个成员函数在读写时很有用。它们具有相似的语法。它们是

```cpp
OfstreamFileObject.write((char *)&the object, sizeof(the same object));
```

用于向文件中写入，以及

```cpp
IfstreamFileObject.read((char *)&the object, sizeof(the same object));
```

用于从文件中读取。

必须理解，文件的读写是按对象进行的，而不是按元素进行的。一次读或写操作读取或写入完整对象。对象甚至可以是程序 13.4 中的 struct student 变量。

> 从键盘读取对象并将其写入屏幕是按元素进行的。

需要相应的语句从键盘读取并构造对象以向文件提供输入，即，首先必须读取 student 对象，然后写入文件。同样，在从文件读取后，需要将对象写入屏幕。在这里，从键盘读取对象和将其写入屏幕都是按元素进行的。只有在从文件读取或写入文件时，才按对象进行读写。

## 13.7.3 关闭二进制文件

关闭二进制文件与关闭文本文件类似。需要 close() 函数来关闭二进制文件。

查看取自程序 13.4 的语句。

```cpp
MCA_StudFile_Out.close();
```

关闭文件的语法是

```cpp
FileObject.close()
```

它还释放文件句柄并刷新分配的缓冲区，如文本文件的情况一样。

## 13.7.4 使用二进制文件

让我们考虑一个 student 结构体的示例。它包含以下实体：学号、姓名、地址，以及学生选择的五个科目的数组。有两个简单程序；程序 13.4 允许用户将一些学生的详细信息添加到学生文件中，程序 13.5 显示数据。打开文件时使用了 open 方法和构造函数。因此，这再次证明两种方法产生相同的结果。程序中使用的 fail() 和 eof() 函数在第 13.8 节中进行了说明。

> 对于商业编程，二进制文件是通常的选择。

```text
Enter name: Steff
Enter address: Germany
Do you want to continue? (y/n): n
```

### PROGRAM 13.5 Reading from a binary file

```cpp
//ReadFile.cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

struct student
{
    int RollNo;
    char Name[30];
    char Address[40];
};

void WriteStudent(student TempStud)
{
    cout << "\n The roll no.: ";
    cout << TempStud.RollNo;
    cout << "\n The name: ";
    cout << TempStud.Name;
    cout << "\n The address: ";
    cout << TempStud.Address;
    cout << "\n";
}

int main()
{
    struct student MCA_Student_In;
    ifstream MCA_StudFile_In("MCA.dat", ios::in | ios::binary);
    while(!MCA_StudFile_In.eof())
    {
        MCA_StudFile_In.read((char*) &MCA_Student_In, sizeof(struct student));

        if(MCA_StudFile_In.fail())
            break;

        WriteStudent(MCA_Student_In);
    }

    MCA_StudFile_In.close();
    return 0;
}
```

```text
The roll no.: 1
The name: Lara
The address: West Indies

The roll no.: 2
The name: Ranatunga
The address: Sri Lanka

The roll no.: 3
The name: Steffi
The address: Germany
```

