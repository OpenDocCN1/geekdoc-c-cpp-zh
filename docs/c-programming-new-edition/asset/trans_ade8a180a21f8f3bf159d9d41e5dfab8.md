

- 安装完成后，打开 Code::Blocks。

## 9.11.2. C 程序的基本结构

```c
// Preprocessor Directives
#include <stdio.h> // Include necessary libraries
// Main Function
int main()
{
// Declarations (Variable and Function Declarations)
// Statements (Executable code)
return 0; // Return statement (Exit status)
}
```

- **预处理器指令：** 这些行以 # 开头，用于包含库并执行其他预处理任务。
- **main()：** 这是程序执行开始的主函数。
- **声明：** 在这里声明程序中将使用的变量和函数。
- **语句：** 这些是执行程序实际工作的可执行语句。
- **return 0;：** 此行用于以状态码 0 退出程序，表示执行成功。

## 9.11.3. 格式说明符

格式说明符用于在 C 中指定要使用 `printf` 和 `scanf` 等函数打印或读取的变量的数据类型。常见的格式说明符包括：

- `%d`：整数
- `%f`：浮点数或双精度
- `%c`：字符
- `%s`：字符串

- `#include <stdio.h>`：此行包含标准输入/输出库，该库提供了如 `printf` 用于向控制台打印的函数。
- `int main()`：这是程序的起点。每个 C 程序都必须有 main 函数，执行从这里开始。`int` 是返回类型，表示 main 函数在完成时会返回一个整数值。
- `{}`：这些大括号括住 main 函数的主体，其中放置程序的语句。
- `printf("Hello, World!\n");`：此行使用 `printf` 函数向控制台打印文本“Hello, World!”。`\n` 表示换行符，将光标移动到下一行。
- `return 0;`：此行返回整数值 0，表示程序已成功执行。在 C 中，返回值为 0 通常表示成功。

要编译和运行此程序，您需要在系统上安装 C 编译器，例如 GCC。将代码保存为 .c 扩展名的文件（例如 hello.c），然后使用以下命令编译和运行它：

- **输出：**
  
  `gcc hello.c -o hello` # 编译程序
  
  `./hello` # 运行编译后的程序

- **实践 3：** 编写一个 c 程序来计算矩形的面积、矩形的周长和矩形的对角线。

- **解决方案：**

```c
#include <stdio.h>
#include <math.h>

int main()
{
    double length, width, area, perimeter, diagonal;
    // Input the length and width of the rectangle
    printf("Enter the length of the rectangle: ");
    scanf("%lf", &length);
    printf("Enter the width of the rectangle: ");
    scanf("%lf", &width);
```

```c
// Calculate the area, perimeter, and diagonal
area = length * width;
perimeter = 2 * (length + width);
diagonal = sqrt(length * length + width * width);
// Display the results
printf("Area of the rectangle: %.2lf\n", area);
printf("Perimeter of the rectangle: %.2lf\n", perimeter);
printf("Diagonal of the rectangle: %.2lf\n", diagonal);
return 0;
}
```

- **实践 4：** 编写一个 c 程序来计算正方形的面积、正方形的周长和正方形的对角线。

- **解决方案：**

```c
#include <stdio.h>
#include <math.h>
int main()
{
double side, area, perimeter, diagonal;
// Input the side length of the square
printf("Enter the side length of the square: ");
scanf("%lf", &side);
// Calculate the area, perimeter, and diagonal
area = side * side;
perimeter = 4 * side;
diagonal = side * sqrt(2);
// Display the results
printf("Area of the square: %.2lf\n", area);
printf("Perimeter of the square: %.2lf\n", perimeter);
printf("Diagonal of the square: %.2lf\n", diagonal);
return 0;
}
```

- **实践 5：** 编写一个 c 程序来计算圆柱体的总面积

和圆柱体的体积。

- 解决方案：

```c
#include <stdio.h>
#include <math.h>
int main()
{
    double radius, height;
    double pi = 3.14159265359; // Approximate value of Pi
    // Input the radius and height of the cylinder
    printf("Enter the radius of the cylinder: ");
    scanf("%lf", &radius);
    printf("Enter the height of the cylinder: ");
    scanf("%lf", &height);
    // Calculate the total surface area of the cylinder
    double surface_area = 2 * pi * radius * (radius + height);
    // Calculate the volume of the cylinder
    double volume = pi * pow(radius, 2) * height;
    // Display the results
    printf("Total surface area of the cylinder: %.2f square units\n", surface_area);
    printf("Volume of the cylinder: %.2f cubic units\n", volume);
    return 0;
}
```

- 实践 6：车辆在 t 秒内行驶的总距离由距离 s = ut+1/2at² 给出，其中‘u’和‘a’分别是初速度（m/sec.）和加速度（m/sec²）。编写一个 C 程序来求给定‘u’和‘a’值时，车辆在时间间隔的规律间隔内行驶的距离。程序应为用户提供灵活性以选择自己的时间间隔并对不同的‘u’和‘a’值重复计算。

```c
#include <stdio.h>
int main()
{
```

```c
double u, a, t, distance;
int num_intervals;
printf("Enter initial velocity (u) in m/sec: ");
scanf("%lf", &u);
printf("Enter acceleration (a) in m/sec^2: ");
scanf("%lf", &a);
printf("Enter the number of time intervals: ");
scanf("%d", &num_intervals);
for (int i = 1; i <= num_intervals; i++)
{
printf("Enter time interval %d in seconds: ", i);
scanf("%lf", &t);
distance = u * t + 0.5 * a * t * t;
printf("Distance traveled at time %.2lf seconds: %.2lf meters\n", t, distance);
}
return 0;
}
```

- 实践 7：编写一个 C 程序，从用户处接收两个整数操作数和一个运算符，执行操作然后打印结果。（考虑运算符 +, -, /, % 并使用 Switch 语句）

- 解决方案：

```c
#include <stdio.h>
int main()
{
int operand1, operand2;
char operator;
printf("Enter two integer operands: ");
scanf("%d %d", &operand1, &operand2);
printf("Enter an operator (+, -, *, /, %%): ");
scanf(" %c", &operator); // Notice the space before %c to consume any
```

```c
leading whitespace.
    switch (operator)
    {
    case '+':
    printf("Result: %d + %d = %d\n", operand1, operand2, operand1 + operand2);
    break;
    case '-':
    printf("Result: %d - %d = %d\n", operand1, operand2, operand1 - operand2);
    break;
    case '*':
    printf("Result: %d * %d = %d\n", operand1, operand2, operand1 * operand2);
    break;
    case '/':
    if (operand2 != 0)
    {
    printf("Result: %d / %d = %.2lf\n", operand1, operand2, (double) operand1 / operand2);
    }
    else
    {
    printf("Error: Division by zero is not allowed.\n");
    }
    break;
    case '%':
    if (operand2 != 0)
    {
    printf("Result: %d %% %d = %d\n", operand1, operand2, operand1 % operand2);
    }
```

```c
else
{
printf("Error: Modulo by zero is not allowed.\n");
}
break;
default:
printf("Error: Invalid operator entered.\n");
}
return 0;
}
```

- **实践 8：** 编写一个 C 程序来求正整数各位数字之和。
- **解决方案：**

```c
#include <stdio.h>
int main()
{
int num, sum = 0, digit;
// Input a positive integer
printf("Enter a positive integer: ");
scanf("%d", &num);
// Check if the input is a positive integer
if (num < 0)
{
printf("Please enter a positive integer.\n");
return 1; // Exit with an error code
}
// Calculate the sum of individual digits
while (num > 0)
{
digit = num % 10; // Get the last digit
sum += digit; // Add the digit to the sum
num /= 10; // Remove the last digit
```

```c
}
// Display the sum of digits
printf("The sum of individual digits is: %d\n", sum);
return 0; // Exit successfully
}
```

- **实践 9：** 斐波那契数列定义如下：数列中的第一项和第二项为 0 和 1。后续项通过将序列中前两个项相加得到。编写一个 C 程序生成数列的前 n 项。
- **解决方案：**

```c
#include <stdio.h>

int main()
{
    int n, first = 0, second = 1, next, i;
    // Input the number of terms to generate
    printf("Enter the number of terms: ");
    scanf("%d", &n);
    // Check if n is valid
    if (n <= 0)
    {
        printf("Please enter a positive integer for the number of terms.\n");
        return 1; // Exit with an error code
    }
    // Print the first two terms (0 and 1) manually
    printf("Fibonacci Series: %d, %d", first, second);
    // Generate and print the rest of the terms
    for (i = 2; i < n; i++)
    {
        next = first + second;
        printf(", %d", next);
        first = second;
        second = next;
```

