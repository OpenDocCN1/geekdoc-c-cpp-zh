
考虑二进制数 $1111101010001010101_2$。现在，

$1111101010001010101_2 = 111\ 1101\ 0100\ 0101\ 0101_2$

$\qquad\qquad\qquad\quad = 0111\ 1101\ 0100\ 0101\ 0101_2$，在左侧补一个零

$\qquad\qquad\qquad\quad = 7D455_{16}$

因此，$1111101010001010101_2 = 7D455_{16}$。

接下来，要将一个十六进制数转换为等价的二进制数，请将该十六进制数中每个十六进制数字的四位二进制表示写入该数中。例如，

$A7F32_{16} = 1010\ 0111\ 1111\ 0011\ 0010_2$

$\qquad\qquad = 10100111111100110010_2$

因此，$A7F32_{16} = 10100111111100110010_2$。

## 关于文件输入/输出的更多内容

在第3章中，你学习了如何从文件读取数据以及将数据写入文件。本节扩展了该章介绍的概念。

### 二进制文件

在第3章中，你学习了如何让程序从文件读取数据以及将数据写入文件。然而，程序到目前为止使用的文件称为文本文件。文本文件中的数据以字符格式存储。例如，考虑数字45。如果将45存储在文件中，那么它存储为两个字符的序列——字符'4'后跟字符'5'。'4'的八位机器表示为00110100，'5'的八位机器表示为00110101。因此，在文本文件中，45存储为0011010000110101。当C++程序读取该数字时，必须首先将其转换为二进制格式。假设整数表示为16位二进制数。那么45的16位二进制表示为0000000000101101。类似地，当程序将数字45存储到文本文件时，必须首先将其转换为文本格式。因此，从文本文件读取数据以及将数据写入文本文件的效率不高，因为数据必须在文本格式和二进制格式之间相互转换。

另一方面，当数据以二进制格式存储在文件中时，读写数据更快，因为不会在将数据从一种格式转换为另一种格式上浪费时间。这样的文件称为二进制文件。更正式地说，**二进制文件**是数据以二进制格式存储的文件。文本文件中的数据也称为**格式化数据**，而二进制文件中的数据称为**原始数据**。

C++允许程序员创建二进制文件。本节说明如何创建二进制文件，以及如何从二进制文件读取数据。

要创建二进制文件，必须以二进制模式打开文件。假设`outFile`是一个`ofstream`变量（对象）。考虑以下语句：

```cpp
outFile.open("employee.dat", ios::binary);
```

该语句打开文件`employee.dat`。该文件中的数据将以其二进制格式写入。因此，文件打开模式`ios::binary`指定以二进制模式打开文件。

接下来，使用流函数`write`将数据写入文件`employee.dat`。使用函数`write`的语法为：

```cpp
fileVariableName.write(reinterpret_cast<const char *> (buffer),
                      sizeof(buffer));
```

其中fileVariableName是用于打开输出文件的对象，第一个参数buffer指定内存中存储数据位置的起始地址。表达式`sizeof(buffer)`指定要写入的数据大小（以字节为单位）。

例如，假设num是一个int变量。以下语句将num的值以二进制格式写入与outFile关联的文件：

```cpp
outFile.write(reinterpret_cast<const char *> (&num),
             sizeof(num));
```

类似地，假设empSalary是一个包含比如100个分量的数组，且分量类型为double。以下语句将整个数组写入与outFile关联的文件：

```cpp
outFile.write(reinterpret_cast<const char *> (empSalary),
             sizeof(empSalary));
```

接下来，我们讨论如何从二进制文件读取数据。从二进制文件读取数据的操作类似于将数据写入二进制文件。首先，必须打开二进制文件。例如，假设inFile是一个ifstream变量，并且程序已经创建了二进制文件employee.dat。以下语句打开该文件：

```cpp
inFile.open("employee.dat");
```

或者：

```cpp
inFile.open("employee.dat", ios::binary);
```

要读取二进制格式的数据，使用流函数`read`。使用函数`read`的语法为：

```cpp
fileVariableName.read(reinterpret_cast<char *> (buffer),
                     sizeof(buffer));
```

第一个参数`buffer`指定内存中要存储数据位置的起始地址。表达式`sizeof(buffer)`指定要读取的数据大小（以字节为单位）。

以下示例中的程序进一步说明如何创建二进制文件以及如何从二进制文件读取数据。

### 示例 E-1

```cpp
//Creating and reading binary files

#include <iostream>
#include <fstream>

using namespace std;

struct studentType
{
    char firstName[15];
    char lastName[15];
    int ID;
};

int main()
{
        //create and initialize an array of students' IDs
    int studentIDs[5] = {111111, 222222, 333333,
                         444444, 555555};             //Line 1

        //declare and initialize the struct newStudent
    studentType newStudent = {"John", "Wilson",
                              777777};                 //Line 2

    ofstream outFile;                                  //Line 3

        //open the output file as a binary file
    outFile.open("ids.dat", ios::binary);              //Line 4

        //write the array in the binary format
    outFile.write(reinterpret_cast<const char *> (studentIDs),
                  sizeof(studentIDs));                 //Line 5
        //write the newStudent data in the binary format
    outFile.write(reinterpret_cast<const char *> (&newStudent),
                  sizeof(newStudent));                 //Line 6

    outFile.close();  //close the file                  //Line 7

    ifstream inFile;                                   //Line 8
    int arrayID[5];                                    //Line 9
    studentType student;                               //Line 10

    //open the input file
    inFile.open("ids.dat");                            //Line 11

    if (!inFile)                                       //Line 12
    {
        cout << "The input file does not exist. "
             << "The program terminates!!!" << endl;   //Line 13
        return 1;                                      //Line 14
    }

    //input the data into the array arrayID
    inFile.read(reinterpret_cast<char *> (arrayID),
                sizeof(arrayID));                      //Line 15
    //output the data from the array arrayID
    for (int i = 0; i < 5; i++)                        //Line 16
        cout << arrayID[i] << " ";                     //Line 17
    cout << endl;                                      //Line 18

    //read the student's data
    inFile.read(reinterpret_cast<char *> (&student),
               sizeof(student));                       //Line 19

    //output studentData
    cout << student.ID << " " << student.firstName
         << " " << student.lastName << endl;           //Line 20

    inFile.close();     //close the file               //Line 21

    return 0;                                          //Line 22
}
```

**示例运行：**

111111 222222 333333 444444 555555
777777 John Wilson

前面程序的输出不言自明。细节留作练习。

> **注意** 在示例 E-1 的程序中，第 2 行的语句声明了`struct`变量`newStudent`，并对其进行了初始化。因为`newStudent`有三个分量，而我们希望初始化所有分量，所以在花括号中指定了三个用逗号分隔的值。换句话说，`struct`变量也可以在声明时初始化。

以下示例中的程序进一步说明如何创建二进制文件，然后从二进制文件读取数据。

