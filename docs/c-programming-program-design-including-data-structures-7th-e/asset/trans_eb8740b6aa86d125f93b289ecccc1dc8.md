
要创建二进制文件，必须以二进制模式打开该文件。假设 outFile 是一个 ofstream 变量（对象）。考虑以下语句：

```cpp
outFile.open("employee.dat", ios::binary);
```

该语句打开文件 employee.dat。此文件中的数据将以其二进制格式写入。因此，文件打开模式 ios::binary 指定以二进制模式打开该文件。

接下来，使用流函数 write 将数据写入文件 employee.dat。使用函数 write 的语法如下：

```cpp
fileVariableName.write(reinterpret_cast<const char *> (buffer),
                       sizeof(buffer));
```

其中 fileVariableName 是用于打开输出文件的对象，第一个参数 buffer 指定数据在内存中存储位置的起始地址。表达式 sizeof(buffer) 指定要写入数据的大小（以字节为单位）。

例如，假设 num 是一个 int 变量。以下语句将 num 的值以二进制格式写入与 outFile 关联的文件：

```cpp
outFile.write(reinterpret_cast<const char *> (&num),
             sizeof(num));
```

类似地，假设 empSalary 是一个包含比如 100 个元素的数组，且元素类型为 double。以下语句将整个数组写入与 outFile 关联的文件：

```cpp
outFile.write(reinterpret_cast<const char *> (empSalary),
             sizeof(empSalary));
```

接下来，我们讨论如何从二进制文件读取数据。从二进制文件读取数据的操作类似于向二进制文件写入数据。首先，必须打开二进制文件。例如，假设 inFile 是一个 ifstream 变量，并且程序已经创建了二进制文件 employee.dat。以下语句打开此文件：

```cpp
inFile.open("employee.dat");
```

或者：

```cpp
inFile.open("employee.dat", ios::binary);
```

要以二进制格式读取数据，使用流函数 read。使用函数 read 的语法如下：

```cpp
fileVariableName.read(reinterpret_cast<char *> (buffer),
                      sizeof(buffer));
```

第一个参数 `buffer` 指定数据要存储到内存中位置的起始地址。表达式 `sizeof(buffer)` 指定要读取数据的大小（以字节为单位）。

以下示例中的程序进一步说明了如何创建二进制文件以及如何从二进制文件读取数据。

## 示例 E-1

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
    int studentIDs[5] = {11111, 222222, 333333,
                         444444, 555555};                  //Line 1

    //declare and initialize the struct newStudent
    studentType newStudent = {"John", "Wilson",
                              777777};                     //Line 2

    ofstream outFile;                                     //Line 3

    //open the output file as a binary file
    outFile.open("ids.dat", ios::binary);                 //Line 4

    //write the array in the binary format
    outFile.write(reinterpret_cast<const char *> (studentIDs),
                  sizeof(studentIDs));                    //Line 5
    //write the newStudent data in the binary format
    outFile.write(reinterpret_cast<const char *> (&newStudent),
                  sizeof(newStudent));                    //Line 6

    outFile.close();  //close the file                  //Line 7

    ifstream inFile;                                      //Line 8
    int arrayID[5];                                       //Line 9
    studentType student;                                  //Line 10

    //open the input file
    inFile.open("ids.dat");                                      //Line 11

    if (!inFile)                                                   //Line 12
    {
        cout << "The input file does not exist.";
        cout << "The program terminates!!!!" << endl;              //Line 13
        return 1;                                                   //Line 14
    }

    //input the data into the array arrayID
    inFile.read(reinterpret_cast<char *> (arrayID),
                sizeof(arrayID));                                  //Line 15
    //output the data of the array arrayID
    for (int i = 0; i < 5; i++)                                    //Line 16
        cout << arrayID[i] << " ";                                 //Line 17
    cout << endl;                                                   //Line 18

    //read the student's data
    inFile.read(reinterpret_cast<char *> (&student),
                sizeof(student));                                  //Line 19

    //output studentData
    cout << student.ID << " " << student.firstName
         << " " << student.lastName << endl;                       //Line 20

    inFile.close();    //close the file                              //Line 21

    return 0;                                                        //Line 22
}
```

### 示例运行：

```text
11111 222222 333333 444444 555555
777777 John Wilson
```

前面程序的输出不言自明。详细内容留作练习。

> **注意**  在示例 E-1 的程序中，第 2 行的语句声明了 `struct` 变量 `newStudent` 并对其进行了初始化。因为 `newStudent` 有三个成员，而我们希望初始化所有成员，所以在花括号中指定了三个用逗号分隔的值。换句话说，`struct` 变量也可以在声明时进行初始化。

以下示例中的程序进一步说明了如何创建二进制文件，然后从这些二进制文件读取数据。

## 示例 E-2

```cpp
//Creating and reading a binary file consisting of
//bank customers' data

#include <iostream>
#include <fstream>
#include <iomanip>

using namespace std;

struct customerType
{
        char firstName[15];
        char lastName[15];
        int ID;
        double balance;
};

int main()
{
        customerType cust;                              //Line 1
        ifstream inFile;                                //Line 2
        ofstream outFile;                               //Line 3

        inFile.open("customerData.txt");                //Line 4

        if (!inFile)                                    //Line 5
        {
                cout << "The input file does not exist. "
                     << "The program terminates!!!!" << endl; //Line 6
                return 1;                               //Line 7
        }

        outFile.open("customer.dat", ios::binary);      //Line 8

        inFile >> cust.ID >> cust.firstName >> cust.lastName
               >> cust.balance;                         //Line 9

        while (inFile)                                  //Line 10
        {
                outFile.write(reinterpret_cast<const char *> (&cust),
                              sizeof(cust));            //Line 11
                inFile >> cust.ID >> cust.firstName >> cust.lastName
                       >> cust.balance;                 //Line 12
        }

        inFile.close();                                 //Line 13
        inFile.clear();                                 //Line 14
        outFile.close();                                //Line 15

        inFile.open("customer.dat", ios::binary);                 //Line 16

        if (!inFile)                                              //Line 17
        {
            cout << "The input file does not exist. "
                 << "The program terminates!!!" << endl;          //Line 18
            return 1;                                             //Line 19
        }

        cout << left << setw(8) << "ID"
             << setw(16) << "First Name"
             << setw(16) << "Last Name"
             << setw(10) << " Balance" << endl;                   //Line 20
        cout << fixed << showpoint << setprecision(2);            //Line 21

            //read and output the data from the binary
            //file customer.dat
        inFile.read(reinterpret_cast<char *> (&cust),
                    sizeof(cust));                                //Line 22
        while (inFile)                                            //Line 23
        {
            cout << left << setw(8) << cust.ID
                 << setw(16) << cust.firstName
                 << setw(16) << cust.lastName
                 << right << setw(10) << cust.balance
                 << endl;                                         //Line 24
            inFile.read(reinterpret_cast<char *> (&cust),
                        sizeof(cust));                            //Line 25
        }

        inFile.close();       //close the file                 //Line 26

        return 0;                                                 //Line 27
}
```

### 示例运行：

| ID | 名 | 姓 | 余额 |
| --- | --- | --- | --- |
| 77234 | Ashley | White | 4563.50 |
| 12345 | Brad | Smith | 128923.45 |
| 87123 | Lisa | Johnson | 2345.93 |
| 81234 | Sheila | Robinson | 674.00 |
| 11111 | Rita | Gupta | 14863.50 |
| 23422 | Ajay | Kumar | 72682.90 |
| 22222 | Jose | Ramey | 25345.35 |
| 54234 | Sheila | Duffy | 65222.00 |
| 55555 | Tommy | Pitts | 892.85 |
| 23452 | Salma | Quade | 2812.90 |
| 32657 | Jennifer | Ackerman | 9823.89 |
| 82722 | Steve | Sharma | 78932.00 |

