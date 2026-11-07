
### 程序 2.4 使用无符号整数

```cpp
1 /************************************************
2  * Finding the total value of a set of coins
3  ************************************************/
4 #include <iostream>
5 using namespace std;
6
7 int main ()
8 {
9     // Defining constants
10     const unsigned int pennyValue = 1;
11     const unsigned int nickelValue = 5;
12     const unsigned int dimeValue = 10;
13     const unsigned int quarterValue = 25;
14     const unsigned int dollarValue = 100;
15     // Defining variables (number of each coin)
16     unsigned int pennies;
17     unsigned int nickels;
18     unsigned int dimes;
19     unsigned int quarters;
20     unsigned int dollars;
21     // Defining total value
22     unsigned long totalValue;
23     // Inputting number of different coins
24     cout << "Enter the number of pennies: ";
25     cin >> pennies;
26     cout << "Enter the number of nickels: ";
27     cin >> nickels;
28     cout << "Enter the number of dimes: ";
29     cin >> dimes;
30     cout << "Enter the number of quarters: ";
31     cin >> quarters;
32     cout << "Enter the number of dollars: ";
33     cin >> dollars;
34     // Calculating total value
35     totalValue = pennies * pennyValue + nickels * nickelValue +
36         dimes * dimeValue + quarters * quarterValue + dollars * dollarValue;
37     // Outputting result
38     cout << "The total value is: " << totalValue << " pennies.";
39     return 0;
40 }
```

运行：
```text
Enter the number of pennies: 20
Enter the number of nickels: 5
Enter the number of dimes: 10
Enter the number of quarters: 4
Enter the number of dollars: 6
The total value is: 845 pennies.
```

### 程序 2.5 在程序中使用有符号整数

```cpp
/*********************************************************
 * Finding the balance of an account after three transactions    *
 **********************************************************/
#include <iostream>
using namespace std;

int main ()
{
  // Definition of variables
  int balance = 0;
  int transaction;
  // Inputting first transaction and adjusting the balance
  cout << "Enter the value of the first transaction: ";
  cin >> transaction;
  balance = balance + transaction;
  // Inputting second transaction and adjusting the balance
  cout << "Enter the value of the second transaction: ";
  cin >> transaction;
  balance = balance + transaction;
  // Inputting third transaction and adjusting the balance
  cout << "Enter the value of the third transaction: ";
  cin >> transaction;
  balance = balance + transaction;
  // Outputting the final balance
  cout << "The total balance is: " << balance << " dollars. ";
  return 0;
}
```

运行：
```text
Enter the value of the first transaction: 70
Enter the value of the second transaction: -50
Enter the value of the third transaction: 35
The total balance in your account is: 55 dollars.
```

### 示例 2.11

在处理银行交易时，我们需要考虑有符号整数。存款是正值交易；取款是负值交易。程序 2.5 展示了当账户初始余额为零美元时，经过三笔交易后的账户余额。注意，由于我们同时使用正整数和负整数，即使余额为负，我们也允许每位客户取款。

### 示例 2.12

在本书后面，我们会进一步讨论每种类型的大小以及最大值和最小值。现在，我们编写一个小程序（程序 2.6），并使用 sizeof 运算符来查找我们所用平台上整数数据类型的大小。这有助于我们避免使用超出该类型范围的数据值。

### 程序 2.6 查找整数类型的大小

```cpp
/****************************************************************
 * A program to find the size of all three integer types         *
 ****************************************************************/
#include <iostream>
using namespace std;

int main()
{
    cout << "Size of short int is " << sizeof (short int) << " bytes." << endl;
    cout << "Size of int is " << sizeof (int) << " bytes." << endl;
    cout << "Size of long int is " << sizeof (long int) << " bytes." << endl;
    return 0;
}
```

运行：
```text
Size of short int: 2 bytes.
Size of int: 4 bytes.
Size of long int: 4 bytes.
```

注意，在我们用来运行该程序的计算机上，**int** 和 **long int** 的大小相同。

## 整数字面量

当我们在程序中显式使用任何类型的值时，该值称为字面量。**整数字面量**在程序中使用时具有常量值；程序执行时其值不会改变。如果程序员没有定义整数字面量的大小和符号，系统会使用能够容纳该值的最小大小（**int** 或 **long**）。如果该整数为正，则该字面量是**无符号**的；如果为负，则该字面量是**有符号**的。程序员可以使用表 2.4 中定义的后缀来显式定义字面量的大小和符号。

注意，short int 不用于字面量。默认值是 int（无后缀）。要告诉编译器我们需要 long，可以使用后缀 l 或 L（小写或大写）。数值字面量默认是有符号的：要显式说明我们希望它们无符号，需要使用后缀 u 或 U（小写或大写）。但是请注意，我们不推荐使用小写格式（l 或 u）。前者太容易与数字 1 混淆。

> 要显式定义整数字面量的大小或符号，我们使用后缀。

**表 2.4** 用于显式指定整数字面量大小和符号的后缀

| 大小 | 后缀 | 符号 | 后缀 |
|---|---|---|---|
| int | 无 | 有符号 int 或 有符号 long | 无 |
| long | l 或 L | 无符号 int 或 无符号 long | u 或 U |

### 示例 2.13

下面展示了我们将整数用作字面量时仅有的四种情况：

```cpp
1234        // The system uses signed integer
1234U       // The system uses unsigned integer
1234L       // The system uses signed long int
1234UL      // The system uses unsigned long int
```

整数字面量可以用于两个目的。它们既可以在计算中作为独立值使用，也可以用于初始化变量。

### 用于初始化的整数字面量

当我们声明变量时，可以将其初始化为某个值。这并不意味着之后不能更改变量的值。它只是意味着，如果没有给变量赋新值，该变量将保持初始值。在本书后面，我们会讨论变量的默认初始化值，但在那之前，我们应记得用适当的值初始化变量。

为了说明为什么在使用整数字面量初始化变量时需要小心，让我们运行程序 2.7。

### 程序 2.7 使用整数字面量进行初始化

```cpp
 /****************************************************************
  * Using some literal values as variable initializers             *
  ****************************************************************/
#include <iostream>
using namespace std;

int main()
{
  // Declaration and initialization
  int x = -1245;
  unsigned int y = 1245;
  unsigned int z = -2367;
  unsigned int t = 14.56;
  // Outputting initialized values
  cout << x << endl;
  cout << y << endl;
  cout << z << endl;
  cout << t;
  return 0;
}
```

运行：
```text
Value of x: -1245        // OK.
Value of y: 1245         // OK.
Value of z: 4294964929   // Logical error. A negative value is changed to positive.
Value of t: 14           // The value is truncated.
```

结果表明第 12 行存在逻辑错误。我们将变量 z 定义为无符号整数，并在其中存储了值 -2367。这个数字被解释为 4294964929 并存储在 z 中。我们将在下一章讨论这个逻辑错误，但这并不是我们想要的结果。第 18 行的结果同样令人意外。由于我们将变量 t 定义为无符号整数类型，并在其中存储了一个非整数值，系统通过丢弃小数点后的小数部分将该字面量转换为整数值。大多数严格主义者认为这种情况是逻辑错误。

### 用作独立值的整数字面量

我们还可以在程序中将整数字面量用作独立值。在这种情况下，程序看到的值取决于字面量值及其内容。

### 示例 2.14

程序 2.8 展示了几个测试上述情况的案例。

### 程序 2.8 一些字面量的使用

```cpp
/************************************************************/
/* Using some stand alone literal values                    */
/************************************************************/
#include <iostream>
using namespace std;

int main()
{
    // Variable definition
    int x;
    unsigned long int y;
    // Assignments
    x = 1456;
    y = -14567;
    // Outputs
    cout << x << endl;
    cout << y << endl;
```
