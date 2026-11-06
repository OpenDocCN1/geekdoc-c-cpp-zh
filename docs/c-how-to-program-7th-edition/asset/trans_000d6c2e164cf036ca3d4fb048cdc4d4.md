

- b) 一个名为 `Address` 的结构，其中包含字符数组 `streetAddress[25]`、`city[20]`、`state[3]` 和 `zipCode[6]`。
- c) 结构 `Student`，其中包含数组 `firstName[ 15 ]` 和 `lastName[ 15 ]`，以及一个类型为第 (b) 部分中 `struct Address` 的变量 `homeAddress`。
- d) 结构 `Test`，其中包含 16 个宽度均为 1 位的位字段。位字段的名称为字母 `a` 到 `p`。

### 21.7 请考虑以下结构定义和变量声明：

```c
struct Customer {
    char lastName[ 15 ];
    char firstName[ 15 ];
    int customerNumber;

    struct {
        char phoneNumber[ 11 ];
        char address[ 50 ];
        char city[ 15 ];
        char state[ 3 ];
        char zipCode[ 6 ];
    } personal;

} customerRecord, *customerPtr;

customerPtr = &customerRecord;
```

为以下每个部分分别写出访问相应结构成员的表达式：

- a) 结构 `customerRecord` 的成员 `lastName`。
- b) `customerPtr` 所指向结构的成员 `lastName`。
- c) 结构 `customerRecord` 的成员 `firstName`。
- d) `customerPtr` 所指向结构的成员 `firstName`。
- e) 结构 `customerRecord` 的成员 `customerNumber`。
- f) `customerPtr` 所指向结构的成员 `customerNumber`。
- g) 结构 `customerRecord` 的成员 `personal` 的成员 `phoneNumber`。
- h) `customerPtr` 所指向结构的成员 `personal` 的成员 `phoneNumber`。
- i) 结构 `customerRecord` 的成员 `personal` 的成员 `address`。
- j) `customerPtr` 所指向结构的成员 `personal` 的成员 `address`。
- k) 结构 `customerRecord` 的成员 `personal` 的成员 `city`。
- l) `customerPtr` 所指向结构的成员 `personal` 的成员 `city`。
- m) 结构 `customerRecord` 的成员 `personal` 的成员 `state`。
- n) `customerPtr` 所指向结构的成员 `personal` 的成员 `state`。
- o) 结构 `customerRecord` 的成员 `personal` 的成员 `zipCode`。
- p) `customerPtr` 所指向结构的成员 `personal` 的成员 `zipCode`。

### 21.8（洗牌和发牌）

修改图 21.14，使用图 21.3 所示的高性能洗牌算法对纸牌进行洗牌。以两列格式打印洗牌后的牌组。在每张牌前标明其颜色。

### 21.9（移位并打印整数）

编写一个程序，将整型变量右移 4 位。程序应在移位操作前后，以位的形式打印该整数。你的系统会在空出的位中填入 0 还是 1？

### 21.10（通过位移实现乘法）

将无符号整数左移 1 位，等价于将该值乘以 2。编写函数 `power2`，该函数接受两个整型参数 `number` 和 `pow`，并计算

```
number *= 2^pow
```

使用移位运算符计算结果。程序应以整数和位两种形式打印这些值。

### 21.11（将字符打包到无符号整数中）

左移运算符可用于将两个字符值打包到一个双字节无符号整型变量中。编写一个程序，从键盘输入两个字符，并将它们传递给函数 `packCharacters`。要将两个字符打包到无符号整型变量中，先将第一个字符赋给该无符号变量，将该无符号变量左移 8 位，然后使用按位包含 OR 运算符将该无符号变量与第二个字符组合起来。程序应在字符被打包到无符号变量之前和之后，以位的形式输出这些字符，以证明它们确实已正确打包到无符号变量中。

### 21.12（从无符号整数中解包字符）

使用右移运算符、按位 AND 运算符和掩码，编写函数 `unpackCharacters`，该函数接收练习 21.11 中的无符号整数，并将其解包为两个字符。要从一个双字节无符号整数中解包两个字符，应将该无符号整数与掩码 65280（`11111111 00000000`）组合，然后将结果右移 8 位。将所得值赋给一个 `char` 变量；然后，将该无符号整数与掩码 255（`00000000 11111111`）组合。将结果赋给另一个 `char` 变量。程序应在解包前以位的形式打印无符号整数，然后以位的形式打印这些字符，以确认它们已被正确解包。

### 21.13（将字符打包到无符号整数中）

如果你的系统使用四字节整数，请改写练习 21.11 中的程序，以打包四个字符。

### 21.14（从无符号整数中解包字符）

如果你的系统使用四字节整数，请改写练习 21.12 中的函数 `unpackCharacters`，以解包四个字符。通过在掩码变量中将值 255 左移 8 位 0、1、2 或 3 次（取决于要解包的字节），创建解包这四个字符所需的掩码。

### 21.15（反转位）

编写一个程序，反转无符号整数值中各位的顺序。程序应从用户处输入该值，并调用函数 `reverseBits`，以逆序打印这些位。在位反转前后都以位的形式打印该值，以确认位已被正确反转。

### 21.16（按值传递数组）

编写一个演示按值传递数组的程序。[提示：使用结构。] 在被调用函数中修改数组副本，以证明传递的是副本。

### 21.17（使用 `<cctype>` 函数测试字符）

编写一个程序，从键盘输入一个字符，并使用字符处理库中的每个函数测试该字符。打印每个函数返回的值。

### 21.18

以下程序使用函数 `multiple` 来确定从键盘输入的整数是否是某个整数 X 的倍数。仔细检查函数 `multiple`，然后确定 X 的值。

```cpp
// Exercise 21.18: ex21_18.cpp
// This program determines if a value is a multiple of X.
#include <iostream>
using namespace std;

bool multiple( int );

int main()
{
    int y;

    cout << "Enter an integer between 1 and 32000: ";
    cin >> y;

    if ( multiple( y ) )
        cout << y << " is a multiple of X" << endl;
    else
        cout << y << " is not a multiple of X" << endl;
} // end main

// determine if num is a multiple of X
bool multiple( int num )
{
    bool mult = true;

    for ( int i = 0, mask = 1; i < 10; i++, mask <<= 1 )
        if ( ( num & mask ) != 0 )
        {
            mult = false;
            break;
        } // end if

    return mult;
} // end function multiple
```

### 21.19

以下程序执行什么操作？

```cpp
// Exercise 21.19: ex21_19.cpp
#include <iostream>
using namespace std;

bool mystery( unsigned );

int main()
{
    unsigned x;

    cout << "Enter an integer: ";
    cin >> x;
    cout << boolalpha
         << "The result is " << mystery( x ) << endl;
} // end main

// What does this function do?
bool mystery( unsigned bits )
{
    const int SHIFT = 8 * sizeof( unsigned ) - 1;
    const unsigned MASK = 1 << SHIFT;
    unsigned total = 0;

    for ( int i = 0; i < SHIFT + 1; i++, bits <<= 1 )
        if ( ( bits & MASK ) == MASK )
            ++total;

    return ( total % 2 );
} // end function mystery
```

### 21.20

编写一个程序，使用 `istream` 成员函数 `getline`（如第 15 章所示）将一行文本输入到字符数组 `s[100]` 中。以大写字母和小写字母两种形式输出该行文本。

### 21.21（将字符串转换为整数）

编写一个程序，输入四个表示整数的字符串，将这些字符串转换为整数，计算这些值的总和，并打印四个值的总和。只能使用本章介绍的 C 风格字符串处理技术。

