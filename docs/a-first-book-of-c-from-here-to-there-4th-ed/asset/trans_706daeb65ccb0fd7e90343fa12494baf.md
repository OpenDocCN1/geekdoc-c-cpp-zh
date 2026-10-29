

# 信息点

## 原子数据

迄今为止声明的所有变量都用于存储原子数据值。原子数据值被视为一个完整的实体，不能分解为语言支持的更小的数据类型。例如，虽然整数可以分解为单独的数字，但 C++ 没有数值数字类型。相反，每个整数都被视为一个完整的值，因此被认为是原子数据。因为整数数据类型只支持原子数据值，所以它被称为原子数据类型。正如你所预期的那样，double、char 和 bool 也是原子数据类型。

使用这些变量名，将 45 存储在位置 1652、将 12 存储在位置 2548，并将这两个位置的内容相加的操作，可以通过以下 C++ 语句完成：

```
num1 = 45;
num2 = 12;
total = num1 + num2;
```

其中每个语句都称为赋值语句，因为它告诉计算机将值赋给（存储在）变量。赋值语句总是包含等号（=），并且等号左侧紧跟一个变量名。等号右侧的值会先被确定；然后该值被赋给等号左侧的变量。赋值语句中的空白是为了可读性而插入的。赋值语句将在第 3 章中更详细地解释，但现在只需知道你可以用它们将值存储到变量中即可。

变量名很有用，因为它使程序员不必考虑数据在计算机中物理存储的位置。你只需使用变量名，让编译器担心数据实际存储在内存中的位置。然而，在将值存储到变量之前，C++ 要求明确声明要存储在其中的数据类型。你必须提前告诉编译器，字符变量的名称、整数使用的名称，以及用于存储其他 C++ 数据类型的名称。

## 声明语句

要命名一个变量并指定可以存储在其中的数据类型，你使用声明语句，其一般形式如下：

```
dataType variableName;
```

在此形式中，dataType 指定一个有效的 C++ 数据类型，而 variableName 是你为变量选择的名称。例如，用于保存整数值的变量是通过使用关键字 int 来指定数据类型，并具有以下形式进行声明：

```
int variableName;
```

因此，以下声明语句将 sum 声明为能够存储整数值的变量的名称：

```
int sum;
```

此外，关键字 long 用于指定长整数。例如，语句

```
long datenum;
```

将 datenum 声明为用于存储长整数的变量。当使用 long 限定符时，你也可以包含关键字 int，因此之前的声明也可以写成如下形式：

```
long int datenum;
```

用于保存单精度值的变量是通过使用关键字 float 声明的，而用于保存双精度值的变量是通过使用关键字 double 声明的。例如，以下语句将 firstnum 声明为用于存储单精度数字的变量：

```
float firstnum;
```

类似地，以下语句声明变量 secnum 用于存储双精度数字：

```
double secnum;
```

尽管声明语句可以放在函数的任何位置，但通常它们被分组在一起并放在函数的左大括号之后。然而，变量必须在使用前始终声明，并且像所有 C++ 语句一样，声明语句必须以分号结束。包含在函数左大括号后声明语句的简单 main() 函数具有以下一般形式：

```
#include <iostream>
using namespace std;

int main()
{
    declaration statements;

    other statements;

    return 0;
}
```

程序 2.3 使用此形式声明并使用四个双精度变量，并使用 cout 对象显示其中一个变量的内容。

## 程序 2.3

```
#include <iostream>
using namespace std;
int main()
{
    double grade1; // declare grade1 as a double variable
    double grade2; // declare grade2 as a double variable
    double total;  // declare total as a double variable
    double average; // declare average as a double variable

    grade1 = 85.5;
    grade2 = 97.0;
    total = grade1 + grade2;
    average = total/2.0; // divide the total by 2.0
    cout << "The average grade is " << average << endl;

    return 0;
}
```

程序 2.3 中声明语句的放置很直接，虽然你很快就会看到这四个声明可以合并为单个声明语句。当程序 2.3 运行后，会显示以下输出：

```
The average grade is 91.25
```

请注意，当变量名插入到 cout 语句中时，存储在变量中的值会被放置到输出流并显示出来。

正如整数和实数（单精度、双精度和长双精度）变量必须在使用前声明一样，用于存储单个字符的变量也必须声明。字符变量是通过使用关键字 char 声明的。例如，以下声明指定 ch 是一个字符变量：

```
char ch;
```

程序 2.4 说明了此声明以及使用 cout 显示字符变量中存储的值。

## 数据类型、声明和显示

## 程序 2.4

```
```cpp
#include <iostream>
using namespace std;

int main()
{
    char ch;    // this declares a character variable

    ch = 'a';   // store the letter a in ch
    cout << "The character stored in ch is " << ch << endl;
    ch = 'm';   // now store the letter m in ch
    cout << "The character now stored in ch is " << ch << endl;

    return 0;
}
```
```

当程序 2.4 运行后，会产生以下输出：

```
The character stored in ch is a
The character now stored in ch is m
```

请注意，第一次存储在变量 ch 中的字母是 a，第二次存储的是 m。因为变量一次只能存储一个值，所以将 m 分配给变量会自动覆盖 a 值。

## 多重声明

相同数据类型的变量始终可以分组并使用单个声明语句声明，其常见形式如下：

```
dataType variableList;
```

例如，程序 2.3 中使用的四个单独声明

```
double grade1;
double grade2;
double total;
double average;
```

可以用以下单个声明语句替换：

```
double grade1, grade2, total, average;
```

类似地，两个字符声明

```
char ch;
char key;
```

可以用以下单个声明语句替换：

```
char ch, key;
```

在单个声明语句中声明多个变量需要只给出一次变量的数据类型，用逗号分隔所有变量名，并使用一个分号终止声明。每个逗号后的空格是为了可读性而插入的，并不是必需的。

声明语句也可以用于在已声明的变量中存储值。例如，声明语句

```
int num1 = 15;
```

既声明变量 num1 为整数变量，又将值 15 设置到该变量中。当声明语句用于将值存储到变量中时，变量被称为已初始化。因此，在此示例中，说变量 num1 已初始化为 15 是正确的。

类似地，以下声明语句声明三个双精度变量并初始化其中两个：

```
double grade1 = 87.0;
double grade2 = 93.5;
double total;
```

使用常量和/或先前已初始化变量的表达式也可以用作初始化器。因此，表达式 87.5 - 3.0 * factor 只有在 factor 已被声明并先前初始化时才是有效的初始化器。此外，可以使用单个声明语句进行多次初始化。然而，这些声明应清晰明了，如果可能的话应简短，如声明 int x, y=0, z=0; 程序 2.3 使用声明初始化后变为程序 2.3a。

## 程序 2.3a

```
#include <iostream>
using namespace std;

int main()
{
    double grade1 = 85.5;
    double grade2 = 97.0;
    double total, average;

    total = grade1 + grade2;
    average = total/2.0;  // divide the total by 2.0
    cout << "The average grade is " << average << endl;

    return 0;
}
```

