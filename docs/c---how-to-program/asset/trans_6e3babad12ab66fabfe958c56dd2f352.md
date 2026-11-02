
### 14.2.2 使用 | 重定向输入

第二种重定向输入的方法是管道。管道 (|) 会将一个程序的输出重定向为另一个程序的输入。假设程序 random 输出一系列随机整数；random 的输出可以直接通过命令行“管道传输”给程序 sum

```
$ random | sum
```

这会计算出 random 所产生的整数之和。在 Linux/UNIX、Windows 和 OS X 中，管道操作是完全相同的。

### 14.2.3 重定向输出

可以通过使用重定向输出符号 (>) 将标准输出流重定向到文件。例如，要将程序 random 的输出重定向到文件 out，请使用

```
$ random > out
```

最后，可以通过使用追加输出符号 (>>) 将程序输出追加到现有文件的末尾。例如，要将前一条命令行中创建的文件 out 追加程序 random 的输出，请使用以下命令行

```
$ random >> out
```

### 14.3 可变长度参数列表

可以创建接收不确定数量参数的函数。文本中的大多数程序都使用了标准库函数 printf，正如你所知，它接受可变数量的参数。最少，printf 必须接收一个字符串作为其第一个参数，但 printf 可以接收任意数量的额外参数。printf 的函数原型为

```c
int printf(const char *format, ...);
```

函数原型中的省略号 (...) 表示函数接收任意类型的可变数量参数。省略号必须始终放在参数列表的末尾。

可变参数头文件 <stdarg.h>（图 14.1）中的宏和定义提供了构建具有可变长度参数列表的函数所需的功能。图 14.2 演示了接收可变数量参数的函数 average（第 25–39 行）。average 的第一个参数始终是要求平均值的数值个数。

图 14.1 | stdarg.h 可变长度参数列表类型和宏。（第 1 部分，共 2 部分。）

| 标识符 | 说明 |
|------------|-------------|
| va_list | 适合保存宏 va_start、va_arg 和 va_end 所需信息的类型。要访问可变长度参数列表中的参数，必须定义 va_list 类型的对象。 |
| va_start | 在可以访问可变长度参数列表的参数之前调用的宏。该宏初始化使用 va_list 声明的对象，以便由 va_arg 和 va_end 宏使用。 |
| va_arg | 宏展开为可变长度参数列表中下一个参数的值——该值具有作为宏第二个参数指定的类型。每次调用 va_arg 都会修改使用 va_list 声明的对象，使其指向列表中的下一个参数。 |
| va_end | 一个宏，用于促进从其可变长度参数列表已被 va_start 宏引用的函数正常返回。 |

图 14.1 | stdarg.h 可变长度参数列表类型和宏。（第 2 部分，共 2 部分。）

图 14.2 | 使用可变长度参数列表。（第 1 部分，共 2 部分。）

```c
// Fig. 14.2: fig14_02.c
// Using variable-length argument lists
#include <stdio.h>
#include <stdarg.h>

double average(int i, ...); // prototype

int main(void)
{
    double w = 37.5;
    double x = 22.5;
    double y = 1.7;
    double z = 10.2;

    printf("%s%5.1f\n%s%5.1f\n%s%5.1f\n%s%5.1f\n\n",
           "w = ", w, "x = ", x, "y = ", y, "z = ", z);
    printf("%s%5.3f\n%s%5.3f\n%s%5.3f\n",
           "The average of w and x is ", average(2, w, x),
           "The average of w, x, and y is ", average(3, w, x, y),
           "The average of w, x, y, and z is ",
           average(4, w, x, y, z));
}

// calculate average
double average(int i, ...)
{
    double total = 0; // initialize total
    va_list ap; // stores information needed by va_start and va_end

    va_start(ap, i); // initializes the va_list object

    // process variable-length argument list
    for (int j = 1; j <= i; j++) {
        total += va_arg(ap, double);
    }

    va_end(ap); // clean up variable-length argument list
    return total / i; // calculate average
}
```

```
w = 37.5
x = 22.5
y = 1.7
z = 10.2

The average of w and x is 30.000
The average of w, x, and y is 20.567
The average of w, x, y, and z is 17.975
```

图 14.2 | 使用可变长度参数列表。（第 2 部分，共 2 部分。）

函数 average（第 25–39 行）使用了头文件 <stdarg.h> 的所有定义和宏，除了在 C11 中添加的 va_copy（第 E.8.10 节）。类型为 va_list（第 28 行）的对象 ap 由宏 va_start、va_arg 和 va_end 使用来处理函数 average 的可变长度参数列表。该函数首先调用宏 va_start（第 30 行）来初始化对象 ap，以便在 va_arg 和 va_end 中使用。该宏接收两个参数——对象 ap 和省略号之前参数列表中最右边的参数的标识符——本例中为 i（va_start 在此处使用 i 来确定可变长度参数列表的开始位置）。接下来，函数 average 反复将可变长度参数列表中的参数添加到变量 total（第 33–35 行）。要添加到 total 的值是通过调用宏 va_arg 从参数列表中检索的。宏 va_arg 接收两个参数——对象 ap 和参数列表中期望的值的类型——本例中为 double。该宏返回参数的值。函数 average 调用宏 va_end（第 37 行），以对象 ap 作为参数，以便从 average 正常返回到 main。最后，平均值被计算并返回给 main。

> 常见编程错误 14.1
> 将省略号放在函数参数列表中间是语法错误——省略号只能放在参数列表的末尾。

你可能会想，具有可变长度参数列表的函数（如 printf 和函数 scanf）如何知道在每个 va_arg 宏中使用什么类型。答案是，在程序执行时，它们会扫描格式控制字符串中的格式转换说明符，以确定下一个要处理的参数的类型。

### 14.4 使用命令行参数

在许多系统上，可以通过在 main 的参数列表中包含参数 int argc 和 char *argv[] 从命令行向 main 传递参数。参数 argc 接收用户输入的命令行参数的数量。参数 argv 是一个字符串数组，其中存储了实际的命令行参数。命令行参数的常见用途包括向程序传递选项和向程序传递文件名。

图 14.3 将文件逐个字符复制到另一个文件。我们假设该程序的可执行文件名为 `mycopy`。在 Linux/UNIX 系统上，`mycopy` 程序的典型命令行是

```
$ mycopy input output
```

该命令行表示文件 input 要被复制到文件 output。当程序执行时，如果 argc 不是 3（mycopy 算作其中一个参数），程序会打印错误消息并终止。否则，argv 包含字符串 "mycopy"、"input" 和 "output"。命令行上的第二个和第三个参数被程序用作文件名。文件使用函数 fopen 打开。如果两个文件都成功打开，则从文件 input 读取字符并写入文件 output，直到为文件 input 设置了文件结束指示符。然后程序终止。结果是文件 input 的精确副本（如果处理过程中没有发生错误）。有关命令行参数的更多信息，请参阅系统文档。[注意：在 Visual C++ 中，你可以通过右键单击 Solution Explorer 中的项目名称并选择 Properties，然后展开 Configuration Properties，选择 Debugging 并在 Command Arguments 右侧的文本框中输入参数来指定命令行参数。]

```c
// Fig. 14.3: fig14_03.c
// Using command-line arguments
#include <stdio.h>

int main(int argc, char *argv[])
{
    // check number of command-line arguments
    if (argc != 3) {
        puts("Usage: mycopy infile outfile");
    }
    else {
        FILE *inFilePtr; // input file pointer

        // try to open the input file
        if ((inFilePtr = fopen(argv[1], "r")) != NULL) {
            FILE *outFilePtr; // output file pointer

            // try to open the output file
            if ((outFilePtr = fopen(argv[2], "w")) != NULL) {
                int c; // holds characters read from source file

                // read and output characters
                while ((c = fgetc(inFilePtr)) != EOF) {
                    fputc(c, outFilePtr);
                }

                fclose(outFilePtr); // close the output file
            }
            else { // output file could not be opened
                printf("File \"%s\" could not be opened\n", argv[2]);
            }
        }
    }
}
```

**图 14.3** | 使用命令行参数。（第 1 部分，共 2 部分。）
