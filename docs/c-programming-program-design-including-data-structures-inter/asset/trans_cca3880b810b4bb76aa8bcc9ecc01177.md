
## 声明和初始化变量

当声明一个变量时，C++可能不会自动为其放入有意义的值。换句话说，C++可能不会自动初始化变量。例如，int和double变量可能不会像某些编程语言那样被初始化为0。然而，这并不意味着变量在声明后没有值。当声明一个变量时，会为其分配内存。

回顾第1章，主存是一个有序的单元序列，每个单元能够存储一个值。另外，回忆一下机器语言是0和1的序列，即比特。因此，内存单元中的数据是一个比特序列。这些比特不过是电信号，所以当计算机开启时，一些比特为1，一些为0。这些比特的状态取决于系统如何运行。然而，当你指示计算机在内存单元中存储特定值时，比特会根据所存储的数据进行设置。

在数据操作过程中，计算机取出特定单元中存储的值并进行计算。如果你声明了一个变量但没有在其中存储值，内存单元仍然有一个值——通常是这些比特上次使用后的值——而你无法知道这个值是什么。

如果你只声明一个变量而没有指示计算机将数据放入该变量，那么该变量的值就是垃圾值。然而，计算机不会警告我们，而是将内存中的任何值视为合法值，并使用这些内存值进行计算。在表达式中使用未初始化的变量会产生错误的结果。为了避免这些陷阱，C++允许你在声明变量的同时初始化它们。例如，考虑以下C++语句，其中变量先声明然后初始化：

```
int first, second;
char ch;
double x;

first = 13;
second = 10;
ch = ' ';
x = 12.6;
```

你可以使用以下C++语句同时声明并初始化这些变量：

```
int first = 13, second = 10;
char ch = ' ';
double x = 12.6;
```

第一条C++语句声明了两个int变量first和second，并将13存入first，将10存入second。其他语句的含义类似。

例2-17进一步解释了如何将数值数据输入到程序中。

### 例2-17

假设我们有以下语句：

```
int feet;
int inches;
```

假设输入为：

```
23 7
```

接下来，考虑以下语句：

```
cin >> feet >> inches;
```

该语句首先将数字23存入变量feet，然后将数字7存入变量inches。注意，当通过键盘输入这些数字时，它们用一个空格分隔。实际上，它们可以用一个或多个空格、换行甚至制表符分隔。

以下C++程序展示了前面输入语句的效果：

```
// This program illustrates how input statements work.

#include <iostream>

using namespace std;

int main()
{
    int feet;
    int inches;

    cout << "Enter two integers separated by one or more spaces: ";
    cin >> feet >> inches;
    cout << endl;

    cout << "Feet = " << feet << endl;
    cout << "Inches = " << inches << endl;

    return 0;
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Enter two integers separated by one or more spaces: 23 7
Feet = 23
Inches = 7
```

例2-18中的C++程序说明了如何读取字符串和数值数据。

### 例2-18

```cpp
// This program illustrates how to read strings and numeric data.

#include <iostream>
#include <string>

using namespace std;

int main()
{
    string firstName;                          //Line 1
    string lastName;                           //Line 2
    int age;                                   //Line 3
    double weight;                             //Line 4

    cout << "Enter first name, last name, age, "
         << "and weight, separated by spaces."
         << endl;                              //Line 5

    cin >> firstName >> lastName;              //Line 6
    cin >> age >> weight;                      //Line 7

    cout << "Name: " << firstName << " "
         << lastName << endl;                  //Line 8

    cout << "Age: " << age << endl;            //Line 9
    cout << "Weight: " << weight << endl;      //Line 10

    return 0;                                  //Line 11
}
```

**示例运行：** 在此示例运行中，用户输入以阴影显示。

```
Enter first name, last name, age, and weight, separated by spaces.
Sheila Mann 23 120.5
Name: Sheila Mann
Age: 23
Weight: 120.5
```

前面的程序工作如下：第1到第4行的语句声明了string类型的变量firstName和lastName、int类型的age以及double类型的weight。第5行的语句是输出语句，告诉用户要做什么。（这样的输出语句称为提示行。）如示例运行所示，程序的输入是：

```
Sheila Mann 23 120.5
```

第6行的语句首先读取字符串Sheila并存入变量`firstName`，然后跳过Sheila后的空格，读取字符串Mann并存入变量`lastName`。接下来，第7行的语句首先跳过Mann后的空格，读取23并存入变量`age`，然后跳过23后的空格，读取120.5并存入变量`weight`。

第8、9和10行的语句产生示例运行的第三、第四和第五行。

> 在程序执行期间，如果在一行中输入多个值，这些值必须至少用一个空格或制表符分隔。或者，也可以每行输入一个值。

### 变量初始化

记住，初始化变量有两种方式：使用赋值语句和使用读取语句。考虑以下声明：

```
int feet;
int inches;
```

考虑以下两组代码：

```
(a)  feet = 35;
     inches = 6;
     cout << "Total inches = ";
     cout << 12 * feet + inches;

(b)  cout << "Enter feet: ";
     cin >> feet;
     cout << endl;
     cout << "Enter inches: ";
     cin >> inches;
     cout << endl;
     cout << "Total inches = ";
     cout << 12 * feet + inches;
```

在（a）中，feet和inches使用赋值语句初始化，而在（b）中，这些变量使用输入语句初始化。然而，每次执行（a）中的代码时，除非你编辑源代码、更改值、重新编译并运行，否则feet和inches都会被初始化为相同的值。另一方面，在（b）中，每次程序运行时，都会提示你输入feet和inches的值。因此，读取语句比赋值语句灵活得多。

有时需要使用赋值语句来初始化变量。如果变量仅用于内部计算而不用于读取和存储数据，则尤其如此。

回想一下，C++在声明变量时不会自动初始化变量。有些变量可以在声明时初始化，而另一些变量必须使用赋值语句或读取语句进行初始化。

> 注意：当程序编译时，如果程序在使用变量值之前没有正确初始化该变量，一些较新的IDE可能会给出警告消息。在这种情况下，如果你忽略警告并执行程序，程序可能会异常终止并显示错误消息。

> 注意：假设你想使用输入语句将一个字符存入`char`变量。在程序执行期间，当你输入该字符时，不要包含单引号。例如，假设`ch`是一个`char`变量。考虑以下输入语句：
>
> ```
> cin >> ch;
> ```
>
> 如果你想使用此语句将K存入`ch`，在程序执行期间，你只需输入K。类似地，如果你想使用输入语句将字符串存入`string`变量，在程序执行期间，你只需输入字符串，不要包含双引号。

### 例2-19

此示例进一步说明了赋值语句和输入语句如何操作变量。考虑以下声明：

```
int firstNum, secondNum;
double z;
char ch;
string name;
```

另外，假设以下语句按给定顺序执行：

- 1. `firstNum = 4;`
- 2. `secondNum = 2 * firstNum + 6;`
- 3. `z = (firstNum + 1) / 2.0;`
- 4. `ch = 'A';`
- 5. `cin >> secondNum;`
- 6. `cin >> z;`
- 7. `firstNum = 2 * secondNum + static_cast<int>(z);`
- 8. `cin >> name;`
- 9. `secondNum = secondNum + 1;`
- 10. `cin >> ch;`
- 11. `firstNum = firstNum + static_cast<int>(ch);`
- 12. `z = firstNum - z;`
