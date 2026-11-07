
```cpp
int main()
{
   unsigned inputValue; // integral value to print in binary

   cout << "Enter an unsigned integer: ";
   cin >> inputValue;
   displayBits( inputValue );
} // end main

// display bits of an unsigned integer value
void displayBits( unsigned value )
{
   const int SHIFT = 8 * sizeof( unsigned ) - 1;
   const unsigned MASK = 1 << SHIFT;

   cout << setw( 10 ) << value << " = ";

   // display bits
   for ( unsigned i = 1; i <= SHIFT + 1; ++i )
   {
      cout << ( value & MASK ? '1' : '0' );
      value <<= 1; // shift value left by 1

      if ( i % 8 == 0 ) // output a space after 8 bits
         cout << ' ';
   } // end for

   cout << endl;
} // end function displayBits
```

```text
Enter an unsigned integer: 65000
     65000 = 00000000 00000000 11111101 11101000
```

```text
Enter an unsigned integer: 29
     29 = 00000000 00000000 00000000 00011101
```

**图 21.6** | 以位的形式打印无符号整数。（第 2 部分，共 2 部分。）

函数 `displayBits`（第 19–37 行）使用按位与运算符将变量 `value` 与常量 `MASK` 组合。按位与运算符常与一个称为*掩码*的操作数一起使用——掩码是一个将特定位置为 1 的整数值。掩码用于在值中选择其他位的同时*隐藏*某些位。在 `displayBits` 中，第 22 行将常量 `MASK` 赋值为 `1 << SHIFT`。常量 `SHIFT` 的值在第 21 行通过表达式计算得出：

```cpp
8 * sizeof( unsigned ) - 1
```

该表达式将无符号对象在内存中所需的字节数乘以 8（一个字节中的位数），得到存储一个无符号对象所需的总位数，然后再减去 1。在将无符号对象表示为四字节内存的计算机上，`1 << SHIFT` 的位表示为：

```text
10000000 00000000 00000000 00000000
```

左移运算符将值 1 从 `MASK` 中的低位（最右侧）位移到高位（最左侧）位，并从右侧填入 0 位。第 29 行针对变量 `value` 当前最左侧的位打印 1 或 0。假设变量 `value` 包含 65000（00000000 00000000 11111101 11101000）。当使用 `&` 将 `value` 和 `MASK` 组合时，变量 `value` 中除高位以外的所有位都被“屏蔽掉”（隐藏），因为任何位与 0 进行“与”运算都会得到 0。如果最左侧位为 0，则 `value & MASK` 的求值结果为：

```text
00000000 00000000 11111101 11101000    (value)
10000000 00000000 00000000 00000000    (MASK)
---------------------------------------
00000000 00000000 00000000 00000000    (value & MASK)
```

该结果被解释为假，并打印 0。然后第 30 行使用表达式 `value <<= 1`（即 `value = value << 1`）将变量 `value` 左移一位。对变量 `value` 中的每一位重复这些步骤。最终，值为 1 的位会被移到最左侧位的位置，位操作如下：

```text
11111101 11101000 00000000 00000000    (value)
10000000 00000000 00000000 00000000    (MASK)
---------------------------------------
10000000 00000000 00000000 00000000    (value & MASK)
```

由于两个左侧位都是 1，表达式的结果非零（真），并打印 1。图 21.7 总结了使用按位与运算符组合两个位的结果。

> **常见编程错误 21.2**
>
> 将逻辑与运算符（`&&`）用于按位与运算符（`&`），或反过来，都是逻辑错误。

| 位 1 | 位 2 | 位 1 & 位 2 |
|---:|---:|---:|
| 0 | 0 | 0 |
| 1 | 0 | 0 |
| 0 | 1 | 0 |
| 1 | 1 | 1 |

**图 21.7** | 使用按位与运算符（`&`）组合两个位的结果。

图 21.8 的程序演示了按位与运算符、按位包含或运算符、按位异或运算符和按位求补运算符。函数 `displayBits`（第 53–71 行）打印无符号整数值。

```cpp
// Fig. 21.8: fig21_08.cpp
// Bitwise AND, inclusive OR,
// exclusive OR and complement operators.
#include <iostream>
```

**图 21.8** | 按位与、包含或、异或和求补运算符。（第 1 部分，共 3 部分。）

```cpp
#include <iostream>
using namespace std;

void displayBits( unsigned ); // prototype

int main()
{
   unsigned number1;
   unsigned number2;
   unsigned mask;
   unsigned setBits;

   // demonstrate bitwise &
   number1 = 2179876355;
   mask = 1;
   cout << "\nThe result of combining the following\n";
   displayBits( number1 );
   displayBits( mask );
   cout << "using the bitwise AND operator & is\n";
   displayBits( number1 & mask );

   // demonstrate bitwise |
   number1 = 15;
   setBits = 241;
   cout << "\nThe result of combining the following\n";
   displayBits( number1 );
   displayBits( setBits );
   cout << "using the bitwise inclusive OR operator | is\n";
   displayBits( number1 | setBits );

   // demonstrate bitwise exclusive OR
   number1 = 139;
   number2 = 199;
   cout << "\nThe result of combining the following\n";
   displayBits( number1 );
   displayBits( number2 );
   cout << "using the bitwise exclusive OR operator ^ is\n";
   displayBits( number1 ^ number2 );

   // demonstrate bitwise complement
   number1 = 21845;
   cout << "\nThe one's complement of\n";
   displayBits( number1 );
   cout << "is " << endl;
   displayBits( ~number1 );
} // end main

// display bits of an unsigned integer value
void displayBits( unsigned value )
{
   const int SHIFT = 8 * sizeof( unsigned ) - 1;
   const unsigned MASK = 1 << SHIFT;
```

**图 21.8** | 按位与、包含或、异或和求补运算符。（第 2 部分，共 3 部分。）

```cpp
cout << setw( 10 ) << value << " = ";

// display bits
for ( unsigned i = 1; i <= SHIFT + 1; ++i )
{
   cout << ( value & MASK ? '1' : '0' );
   value <<= 1; // shift value left by 1

   if ( i % 8 == 0 ) // output a space after 8 bits
      cout << ' ';
} // end for

cout << endl;
} // end function displayBits
```

```text
The result of combining the following
2179876355 = 10000000 11011110 01000110 00000011
          1 = 00000000 00000000 00000000 00000001

using the bitwise AND operator & is
          1 = 00000000 00000000 00000000 00000001

The result of combining the following
         15 = 00000000 00000000 00000000 00001111
        241 = 00000000 00000000 00000000 11110001
using the bitwise inclusive OR operator | is
        255 = 00000000 00000000 00000000 11111111

The result of combining the following
        139 = 00000000 00000000 00000000 10001011
        199 = 00000000 00000000 00000000 11000111
using the bitwise exclusive OR operator ^ is
         76 = 00000000 00000000 00000000 01001100

The one's complement of
      21845 = 00000000 00000000 01010101 01010101
is
 4294945450 = 11111111 11111111 10101010 10101010
```

**图 21.8** | 按位与、包含或、异或和求补运算符。（第 3 部分，共 3 部分。）

## 按位与运算符（&）

在图 21.8 中，第 18 行将 2179876355（10000000 11011110 01000110 00000011）赋给变量 `number1`，第 19 行将 1（00000000 00000000 00000000 00000001）赋给变量 `mask`。当在表达式 `number1 & mask`（第 24 行）中使用按位与运算符（`&`）组合 `mask` 和 `number1` 时，结果为 00000000 00000000 00000000 00000001。变量 `number1` 中除低位以外的所有位都通过与常量 `MASK` 进行“与”运算而被“屏蔽掉”（隐藏）。

## 按位包含或运算符（|）

按位包含或运算符用于将操作数中的特定位置为 1。在图 21.8 中，第 27 行将 15（00000000 00000000 00000000 00001111）赋给变量 `number1`，第 28 行将 241（00000000 00000000 00000000 11110001）赋给变量 `setBits`。当在表达式 `number1 | setBits`（第 33 行）中使用按位或运算符组合 `number1` 和 `setBits` 时，结果为 255（00000000 00000000 00000000 11111111）。图 21.9 总结了使用按位包含或运算符组合两个位的结果。

> **常见编程错误 21.3**
>
> 将逻辑或运算符（`||`）用于按位或运算符（`|`），或反过来，都是逻辑错误。

![](img/bfd978e7e9b192bab46ec2a89e481263_836_0.png)

| 位 1 | 位 2 | 位 1 \| 位 2 |
|---:|---:|---:|
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 1 |

**图 21.9** | 使用按位包含或运算符（`|`）组合两个位。

## 按位异或运算符（^）

按位异或运算符（`^`）在其两个操作数中对应的位恰好有一个为 1 时，将结果中的每一位设置为 1。在图 21.8 中，第 36–37 行分别将变量 `number1` 和 `number2` 赋值为 139（00000000 00000000 00000000 10001011）和 199（00000000 00000000 00000000 11000111）。当在表达式 `number1 ^ number2`（第 42 行）中使用异或运算符组合这些变量时，结果为 00000000 00000000 00000000 01001100。图 21.10 总结了使用按位异或运算符组合两个位的结果。

| 位 1 | 位 2 | 位 1 ^ 位 2 |
|---:|---:|---:|
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 0 | 1 | 1 |
| 1 | 1 | 0 |

**图 21.10** | 使用按位异或运算符（`^`）组合两个位。

## 按位求补运算符（~）

按位求补运算符（`~`）将其操作数中的所有 1 位在结果中置为 0，并将所有 0 位置为 1——这也称为“对该值取反码”。在图 21.8 中，第 45 行将变量 `number1` 赋值为 21845（00000000 00000000 01010101 01010101）。当表达式 `~number1` 求值时，结果为（11111111 11111111 10101010 10101010）。

图 21.11 演示了左移运算符（`<<`）和右移运算符（`>>`）。函数 `displayBits`（第 27–45 行）打印无符号整数值。

