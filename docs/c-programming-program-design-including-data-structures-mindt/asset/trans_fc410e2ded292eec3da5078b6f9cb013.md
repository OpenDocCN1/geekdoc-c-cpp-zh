
## 示例 E-3

假设你在一个文件中存储了下面这行文本，例如 `digitsAndLetters.txt`：

```text
0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

此外，假设 `inFile` 是一个 `ifstream` 对象，并且已使用对象 `inFile` 打开了文件 `digitsAndLetters.txt`。该行文本的每个字符使用一个字节存储。此外，第一个字符的位置为 0。

| 语句 | 说明 |
|---|---|
| `inFile.seekg(10L, ios::beg);` | 将 `inFile` 的读取位置设置为第 11 个字节（字符），其位置为 10。也就是说，它将读取位置设置在数字 9 之后或字母 A 之前。 |
| `inFile.seekg(5L, ios::cur);` | 将 `inFile` 的读取位置从其当前位置向右移动五个字节。 |
| `inFile.seekg(-6L, ios::end);` | 将 `inFile` 的读取位置设置为从末尾数起的第六个字节（字符）。也就是说，它将读取位置设置在字母 U 之前。 |

下例中的程序进一步说明了函数 `seekg` 和 `seekp` 如何工作。

## 示例 E-4

```cpp
#include <iostream>                         //Line 1
#include <fstream>                          //Line 2

using namespace std;                        //Line 3

int main()                                  //Line 4
{                                           //Line 5
    char ch;                                //Line 6
    ifstream inFile;                        //Line 7

    inFile.open("digitsAndLetters.txt");    //Line 8

    if (!inFile)                            //Line 9
    {                                       //Line 10
        cout << "The input file does not exist. "
             << "The program terminates!!" << endl; //Line 11
        return 1;                           //Line 12
    }                                       //Line 13

    inFile.get(ch);                         //Line 14
    cout << "Line 15: The first byte: " << ch
         << endl;                           //Line 15

    //position the reading marker six bytes to the
    //right of its current position
    inFile.seekg(6L, ios::cur);             //Line 16
    inFile.get(ch);                         //read the character //Line 17
    cout << "Line 18: Current byte read: " << ch
         << endl;                           //Line 18

    //position the reading marker seven bytes
    //from the beginning
    inFile.seekg(7L, ios::beg);             //Line 19
    inFile.get(ch);                         //read the character //Line 20
    cout << "Line 21: Seventh byte from the "
         << "beginning: " << ch << endl;    //Line 21

    //position the reading marker 26 bytes
    //from the end
    inFile.seekg(-26L, ios::end);           //Line 22
    inFile.get(ch);       //read the character //Line 23
    cout << "Line 24: Byte 26 from the end: " << ch
         << endl;                           //Line 24

    return 0;                               //Line 25
}                                           //Line 26
```

### 示例运行：

```text
Line 15: The first byte: 0
Line 18: Current byte read: 7
Line 21: Seventh byte from the beginning: 7
Line 24: Byte 26 from the end: A
```

输入文件包含以下一行文本：

```text
0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ
```

以下程序说明了函数 `seekg` 如何与 `struct` 一起工作。

## 示例 E-5

假设 `customerType` 是一个如下定义的 `struct`：

```cpp
struct customerType
{
    char firstName[15];
    char lastName[15];
    int ID;
    double balance;
};
```

示例 E-2 中的程序创建了二进制文件 customer.dat，其中包含某些客户的数据。你可以使用函数 seekg 将此文件的读取位置移动到任意记录。假设 inFile 是用于打开二进制文件 customer.dat 的 ifstream 对象。

以下语句计算 customerType 结构体的大小，并将其存储在变量 custSize 中：

```cpp
long custSize = sizeof(cust);
```

我们可以使用变量 custSize 的值将读取位置移动到文件中的特定记录。例如，考虑以下语句：

```cpp
inFile.seekg(6 * custSize, ios::beg);
```

此语句将读取位置移动到第六个客户记录之后，也就是第七个客户记录之前。

以下程序进一步说明了函数 seekg 如何与结构体一起工作。

## 示例 E-6

```cpp
//Reading a file randomly

#include <iostream>                         //Line 1
#include <fstream>                          //Line 2
#include <iomanip>                          //Line 3

using namespace std;                        //Line 4

struct customerType                         //Line 5
{                                           //Line 6
    char firstName[15];                     //Line 7
    char lastName[15];                      //Line 8
    int ID;                                 //Line 9
    double balance;                         //Line 10
};                                          //Line 11

void printCustData(const customerType& customer); //Line 12

int main()                                  //Line 13
{                                           //Line 14
    customerType cust;                      //Line 15
    ifstream inFile;                        //Line 16

    long custSize = sizeof(cust);           //Line 17

    inFile.open("customer.dat", ios::binary); //Line 18
    if (!inFile)                            //Line 19
    {                                       //Line 20
        cout << "The input file does not exist. "                 //Line 20
             << "The program terminates!!" << endl;              //Line 21
        return 1;                                                 //Line 22
    }                                                             //Line 23

    cout << fixed << showpoint << setprecision(2);               //Line 24

    //randomly read the records and output them
    inFile.seekg(6 * custSize, ios::beg);                         //Line 25
    inFile.read(reinterpret_cast<char *> (&cust),
                sizeof(cust));                                    //Line 26
    cout << "Seventh customer's data: " << endl;                 //Line 27
    printCustData(cust);                                          //Line 28

    inFile.seekg(8 * custSize, ios::beg);                         //Line 29
    inFile.read(reinterpret_cast<char *> (&cust),
                sizeof(cust));                                    //Line 30
    cout << "Ninth customer's data: " << endl;                   //Line 31
    printCustData(cust);                                          //Line 32

    inFile.seekg(-8 * custSize, ios::end);                        //Line 33
    inFile.read(reinterpret_cast<char *> (&cust),
                sizeof(cust));                                    //Line 34
    cout << "Eighth (from the end) customer's "
         << "data: " << endl;                                    //Line 35
    printCustData(cust);                                          //Line 36

    inFile.close();            //close the file                   //Line 37

    return 0;                                                      //Line 38
}                                                             //Line 39
void printCustData(const customerType& customer)              //Line 40
{
    cout << " ID: " << customer.ID << endl
         << " First Name: " << customer.firstName << endl
         << " Last Name: " << customer.lastName << endl
         << " Account Balance: $" << customer.balance
         << endl;                                              //Line 42
}                                                             //Line 43
```

### 示例运行：

```text
Seventh customer's data:
    ID: 22222
    First Name: Joe
    Last Name: Ramey
    Account Balance: $25345.35
Ninth customer's data:
    ID: 55555
    First Name: Tommy
    Last Name: Pitts
    Account Balance: $892.85
```
