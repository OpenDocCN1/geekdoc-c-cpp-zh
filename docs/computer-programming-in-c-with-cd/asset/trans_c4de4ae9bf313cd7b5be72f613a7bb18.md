
## 调试练习

### Q1. 以下程序的输出是什么？

```cpp
#include<iostream.h>

int main()
{
    int num1, num2, sum;
    cout<<"Enter two numbers: "<< endl;
    cin>>num1;
    cin>>num2;
    sum = num1 + num2;
    cout<<"The sum of the two numbers is: "<<sum;

    return 0;
}
```

答。上述程序的输出如下：

```text
Enter two numbers:
10
35
The sum of the two numbers is: 45
```

### Q2. 以下程序的输出是什么？

```cpp
#include <iostream.h>

int main()
{
    bool a = false;
    cout << "The value of the boolean type variable is: " <<a;
    return 0;
}
```

答。上述程序的输出如下：

```text
The value of the boolean type variable is: 0
```

### Q3. 以下程序的输出是什么？

```cpp
#include <iostream.h>

int main()
{
    struct student
    {
        char standard;
        int roll_num;
    };

    student Johnny;

    Johnny.standard = '8';
    Johnny.roll_num = 22;

    cout << "The student is in " << Johnny.standard << " standard." << endl;
    cout << "The roll number of the student is " << Johnny.roll_num << endl;
    return 0;
}
```

答。上述程序的输出如下：

该学生在上 8 年级。
该学生的学号是 22

### Q4. 以下程序的输出是什么？

```cpp
#include <iostream.h>

int main()
{
    union example
    {
        double num;
        double num2;
    };
    example numbers;
    numbers.num= 10.2665;

    cout << "The value of the numbers.num is: " << numbers.num << endl;
    cout << "The value of the numbers.num2 is: " << numbers.num2 << endl;
    return 0;
}
```

答。上述程序的输出如下：

numbers.num 的值为：10.2665
numbers.num2 的值为：10.2665

### Q5. 以下程序的输出是什么？

```cpp
#include <iostream.h>

int main()
{
    int x = 10, y = 3, sum, sub, mul;
    sum = x + y;
    sub = x - y;
    mul = x * y;
    cout << "Addition of " << x << " and " << y << " is: " << sum << endl;
    cout << "Subtraction of " << x << " and " << y << " is : " << sub << endl;
    cout << "Multiplication of " << x << " and " << y << " is : " << mul << endl;
    return 0;
}
```

**答。** 上述程序的输出如下：

```text
Addition of 10 and 3 is : 13
Subtraction of 10 and 3 is : 7
Multiplication of 10 and 3 is : 30
```

### Q6. 以下程序的输出是什么？

```cpp
#include<iostream.h>

void main()
{
    int num1, num2, num3;
    num1=31 ;
    num2=47;
    num3=num1&num2;
    cout<<"The value of num3 is: "<<num3;
}
```

**答。** 上述程序的输出如下：

```text
The value of num3 is: 15
```

### Q7. 以下程序的输出是什么？

```cpp
#include <iostream.h>

int main()
{
    float num1=56.55, num2=23.25, num3=35.66 ;
    float num;
    num =(num1, num2, num3, num1+num2+num3);
    cout << num << endl;
    return 0;
}
```

**答。** 上述程序的输出如下：

```text
115.459999
```

### Q8. 以下程序的输出是什么？

```cpp
#include <iostream.h>

int i = 5;

int main ( )
{
    int j=i++;
    cout << "Value of variable j is " << j << endl;
    cout << "Value of variable i is " << :: i << endl;
    return 0;
}
```

答。上述程序的输出如下：

```text
Value of variable j is 5
Value of variable i is 6
```

### Q9. 以下程序的输出是什么？

```cpp
#include <iostream.h>

int main()
{
    int i;
    i = 180;
    cout<<"The value of i is: "<<i<<endl;
    i = i >>5;
    cout<<"The value of right shifted 5 times i variable is: "<<i<<endl;
    return 0;
}
```

答。上述程序的输出如下：

```text
The value of i is: 180
The value of right shifted 5 times i variable is: 5
```

### Q10. 以下程序的输出是什么？

```cpp
#include <iostream.h>

int main()
{
    char value1, value2, value3, value4;
    value1 = 'A';
    value2 = value3 = value4 = 'U';
    cout << "First value = " << value1 << endl;
    cout << "Second value = " << value2 << endl;
    cout << "Third value = " << value3 << endl;
    cout << "Fourth value = " << value4 << endl;
    return 0;
}
```

答。上述程序的输出如下：

```text
First value = A
Second value = U
Third value = U
Fourth value = U
```

### Q11. 以下程序的输出是什么？

```cpp
#include <iostream.h>
#define PI 3.14
#define circumference(a) (2*PI*a)

int main()
{
    double p= PI;
    double result;
    cout << " Value of p is " << p << endl;
    result = circumference(4);
    cout << " Value of function macro is " << result << endl;
    return 0;
}
```

答。上述程序的输出如下：

```text
Value of p is 3.14
Value of function macro is 25.12
```

### Q12. 以下程序的输出是什么？

```cpp
#include <iostream.h>

int main()
{
    double value1, value2;
    value1= 12 + 24 / 6;
    value2= 24 - 3 / 6;
    cout << "The value of value1 is " << value1 << endl;
    cout << "The value of value2 is " << value2 << endl;
    return 0;
}
```

答。上述程序的输出如下：

```text
The value of value1 is = 16
The value of value2 is = 12
```

## 02 输入/输出数据与流程控制

### 目标

- 2.1 探索数据输入与输出过程
- 2.2 使用条件语句
- 2.3 使用迭代语句
- 2.4 使用跳转语句
- 2.5 使用 `exit()` 和 `abort()` 函数

程序总是将数据作为输入，处理数据并生成所需输出。程序中的这种数据流动称为输入/输出（I/O）。在编程语言中，条件语句和迭代语句用于控制程序的执行；这称为流程控制。条件语句指定一个条件，以在程序中执行一个代码块；迭代语句则重复执行一个代码块，直到条件求值为真。假设你想显示分数超过 50% 的学生的姓名。在这种情况下，你可以使用条件语句，指定仅显示分数超过 50% 的学生的姓名的条件。另一方面，当你想要显示从 1 到 100 的数字时，可以使用迭代语句。在这种情况下，无需逐个输入所有数字，你可以使用迭代语句，从而无需逐个输入即可显示所有数字。

本章中，你将学习数据输入函数，例如 `getchar()`、`scanf()`、`gets()`，用于从键盘输入数据；以及数据输出函数，例如 `putchar()`、`printf()`、`puts()`，用于在屏幕上显示数据。此外，你还将学习通过 `cin` 和 `cout` 对象进行数据输入和输出。本章介绍操纵器，例如 `endl`、`setw`、`setprecision` 和 `setfill`，用于在屏幕上显示格式化数据。你还将学习各种条件语句，例如 if、if-else、嵌套 if；各种迭代语句，例如 while 循环、do-while 循环、for 循环、嵌套循环；以及跳转语句，例如 break、continue 和 goto。最后，你将讨论 `exit()` 和 `abort()` 函数。

### 2.1 探索数据输入与输出过程

在程序中，数据输入和输出是两个重要过程，分别用于接受输入细节，并在处理这些细节后显示信息。输入和输出函数，例如 `getchar()`、`putchar()`、`gets()`、`puts()`。

```cpp
scanf("%c%d", &ch, &i);
```

在上述语法中，从键盘接收的字符会存储到变量（ch、i）中，这些变量对应于使用 & 运算符获得的变量地址。这些字符会根据指定格式（%c 和 %d）分别以字符值和整数值存储到 ch 和 i 变量中。表 1 列出了一些常用格式说明符：

**表 1：一些常用格式说明符**

| 格式说明符 | 类型 |
|---|---|
| %i | int |
| %d | int（十进制） |
| %c | char |
| %f | float |
| %lf | double |
| %s | string |

printf() 函数根据指定格式将字符串或存储在变量中的值打印到控制台屏幕。例如，我们可以通过两种方式使用 printf() 函数显示字符串数据。第一种方式是在 printf() 函数内传入字符串数据；第二种方式是打印存储在 str 变量中的字符串数据。以下示例展示了 printf() 函数的用法：

```cpp
printf("Test string"); // Example 1

printf("%s",&str); // Example 2
```

在第一个示例中，printf() 函数将字符串作为参数，并在控制台屏幕上打印指定字符串。另一方面，在第二个示例中，printf() 函数接受两个参数。第一个参数是字符串格式说明符（%s），它告诉编译器在控制台屏幕上打印字符串数据；第二个参数是变量 str 的地址，字符串数据存储在该变量对应的内存中。清单 2 展示了 scanf() 和 printf() 函数的用法（你可以在 CD 上 codechapter2 文件夹中的 Function2.cpp 文件里找到此示例）：

### 清单 2：使用 scanf() 和 printf() 函数

```cpp
#include <stdio.h>

int main() {
  int num1,num2;
  printf("Enter first number: ");
  scanf("%d",&num1);
  printf("Enter second number: ");
```
