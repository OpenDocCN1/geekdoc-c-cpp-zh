
```c
else if(strcmp(str1, str2) < 0 )
{
    printf("First < second:   %s %s\n", str1, str2);
}
else
{
    printf("First > second:   %s %s\n", str1, str2);
}

return 0;
}
```

清单 6.1 包含 `main()` 函数，该函数初始化字符指针 `str1` 和 `str2`。接下来，通过调用 `strcmp()` 函数并传入参数 `str1` 和 `str2` 来初始化整数 `num` 的值。

`main()` 函数的下一部分包含条件逻辑，根据 `strcmp()` 函数的值是否为 0、负数或正数来显示消息。输出如下：

```text
String1: abc
String2: abcd
First < second:   abc abcd
```

此外，还有内置的 C 函数 `strnicmp()`，它执行两个字符串的不区分大小写比较，如下所示：

```c
result = strnicmp(str1, str2, 8);
```

`strnicmp()` 的条件逻辑与第 5 章清单 5.18 中 `strcmp()` 的条件逻辑相同。

> 注意 `strnicmp()` 函数是厂商扩展，不是 C 标准的一部分。

## 使用 STRTOK() 对字符串进行标记化

考虑字符串形式为 "Last/First" 的情况，例如 "Smith/John"。任务是将此类字符串拆分为两个独立的字符串：" / " 符号左侧的字符串和右侧的字符串。我们可以通过内置的 C 函数 strtok() 来执行此任务。

strtok() 函数接收指向字符串的指针 (string_ptr) 和要查找的字符（例如 "/"）作为其参数。接下来，我们使用 while 循环在剩余字符串中查找后续标记。

### 清单 6.2：Tokenize.c

```c
#include <stdio.h>
#include <string.h>

char *delim = "/";

void tokenizeString(char *str)
{
    // first token = last name
    char *token = strtok(str, delim);
    char *second = token;
    char *first;
    int count = 0;

    // print token after delimiter
    while (token != NULL)
    {
        token = strtok(NULL, delim);
        first = token;
    }

    printf("NAME: %s %s\n", first, second);
}

int main()
{
    char *str;
    char names[4][20] = {
            "smith/jane",
            "edwards/john",
            "stone/dave",
            "anderson/kenneth",
    };

    for(int i=0; i<4; i++)
    {
        str = names[i];
        tokenizeString(str);
    }

    return 0;
}
```

清单 6.2 从函数 tokenizeString() 开始，该函数调用 strtok() 函数以获取字符串 str 中的第一个标记。此第一个标记被分配给字符串 second，因为它是姓氏（不是名字）。tokenizeString() 的下一部分包含一个循环，反复调用 strtok() 函数，直到读取 str 的末尾。请注意，strtok() 函数的每次调用都被分配给字符串 first。由于 str 中只有两个名字，因此进行此分配是正确的；即 while 循环将在 strtok() 函数的第一次调用后终止。

然而，如果 `str` 包含给定分隔符的多个出现，我们需要将 while 循环替换为以下代码块：

```c
// print token after delimiter
while (token != NULL)
{
    token = strtok(NULL, delim);
    first = token;
    if(++count == 1) break;
}
```

`main()` 函数使用四个按相反顺序排列的名字（例如 “Smith/John”）初始化数组 `names`。`main()` 函数的下一部分包含一个循环，遍历 `names` 数组的元素并调用函数 `tokenizeString()`。输出如下：

```text
NAME: jane smith
NAME: john edwards
NAME: dave stone
NAME: kenneth anderson
```

## 指针、字符串和回文

如果反转后的字符串与初始字符串相同，则该字符串是回文。清单 6.3 显示了 `StringPalindrome.c` 的内容，说明如何确定字符串是否为回文。

### 清单 6.3：StringPalindrome.c

```c
#include <stdio.h>
#include <string.h>

int scanString(char str[])
{
int result = 0;
char *ptr;
int len = strlen(str);

for(int i=0; i<len/2; i++)
{
    if(str[i] != str[len-i-1])
    {
        result = 1;
        break;
    }
}

return result;
}

int main()
{
    int result=0;
    char line1[] = "radar";
    char line2[] = "motion";
    char *results[] = {"YES", "NO"};

    int len1 = strlen(line1);
    int len2 = strlen(line2);

    result = scanString(line1);
    printf("Current Word: %s\n", line1);
    printf("Palindrome:  %s\n", results[result]);

    result = scanString(line2);
    printf("Current Word: %s\n", line2);
    printf("Palindrome:  %s\n", results[result]);

    return 0;
}
```

**清单 6.3** 包含一个 main() 函数，使用相同的硬编码字符字符串 "Hello World" 初始化指针 ptr1 和 str1，然后定义指向变量 `str1` 位置的字符指针 `ptr2`。其余代码由三个 `printf()` 语句组成。

编译并运行 [清单 6.3](#) 中的代码的输出如下：

```
Current Word: radar
Palindrome:  YES
Current Word: motion
Palindrome:   NO
```

## 按引用传递与按值传递

在 [第 4 章](#) 中，曾简要提到过这个主题，在本节中您将看到使用指针将数据结构传递给函数的示例。

在抽象计算机科学术语中，"按引用传递" 和 "按值传递" 之间存在区别。在按值传递的函数调用中，所有参数的本地副本都会被创建，因此函数无法更改调用范围中的任何数据。按引用传递意味着只传递数据的引用，因此函数所做的任何更改都会影响调用者中的实际数据。C 中没有 "按引用传递" 机制，因此这种行为通常通过传递指向实际数据的指针来模拟。在具有按引用传递语法的其他语言（如 C++ 或 C#）中，并不使用指针来实现此目的。

[清单 6.4](#) 显示了 PassByPointer.c 的内容，说明如何按引用和按值传递。

### 清单 6.4：PassByPointer.c

```c
#include <stdio.h>

int addNumbers1(int a, int b);
void addNumbers2(int a, int b, int * sum);

int addNumbers1(int a, int b)
{
    return (a+b);
}

void addNumbers2(int a, int b, int *sum)
{
    *sum = a+b;
}

int main()
{
    int num1=3, num2=5, sum1, *sum2=&sum1;

    sum1 = addNumbers1(num1, num2);
    printf("%d + %d = %d\n", num1, num2, sum1);

    addNumbers2(2*num1, 3*num2, sum2);
    printf("%d + %d = %d\n", 2*num1, 3*num2, *sum2);

    return 0;
}
```

清单 6.4 很简单：它初始化两个整数值变量，声明另一个整数值变量，然后初始化指向第三个变量位置的整数值指针。

接下来，使用 num1 和 num2 调用函数 addNumbers1()，然后使用 2*num1、3*num2 和 sum2 调用函数 addNumbers2()。每次方法调用后，都会打印各种变量的值。

请注意，函数 addNumbers1() 返回一个整数，而函数 addNumbers2() 更新第三个参数 sum 的值（即它不返回值）。整数值变量 sum2 以粗体突出显示，以便您可以轻松跟踪执行顺序并观察结果。

清单 6.4 的输出如下，您可能期望的结果为：

3 + 5 = 8
6 + 15 = 21

## 按指针传递数组

在函数调用的上下文中，数组被视为指向第一个元素的指针。这意味着无法按值传递数组，只能按引用传递。清单 6.5 显示了 PassArrayByPointer.c 的内容，说明如何按引用传递整数数组。

### 清单 6.5：PassArrayByPointer.c

```c
#include <stdio.h>

void multiplyArray2(int factor, int a[], int * result)
{
    for(int i=0; a[i] != '\0'; i++)
    {
        *(result+i) = factor*a[i];
    }
}

int main()
{
    int arr1[] = {1,2,3,4,5}, factor=3, * result=arr1;

    printf("Initial Values:\n");
    for(int i=0; arr1[i] != '\0'; i++)
```
