
```c
{
    printf( "%d ", arr1[i]);
}
printf( "\n" );

multiplyArray2(factor, arr1, result);

printf( "Updated Values:\n" );
for(int i=0; arr1[i] != '\0'; i++)
{
    printf( "%d ", arr1[i]);
}
printf( "\n" );

return 0;
}
```

**清单 6.5** 包含函数 `multiplyArray2()`，它将数组 `a`（该函数的一个参数）的值乘以一个数，而数组 `a` 和这个数都是该函数的参数。数组 `arr1` 更新后的内容可通过第三个参数访问，该参数是指向整数数组的指针。更新后的数组内容也存在于 `arr1` 中，因为数组没有被复制，而是按引用传递。

接下来，`main()` 函数用一些值初始化数组 `arr1`，将值 3 赋给变量 `factor`，然后用 `arr1` 的地址初始化基于指针的变量 `result`。

`main()` 函数包含两个循环，二者都显示数组 `arr1` 中的值。然而，第一个循环打印数组 `arr1` 的初始值，第二个循环打印在调用 `multiplyArray2()` 函数之后数组 `arr1` 的更新值。请注意，该函数会对数组 `arr1` 中每个元素的值执行乘法。

清单 6.5 的输出如下：

```text
Initial Values:
1 2 3 4 5
Updated Values:
3 6 9 12 15
```

## 使用指向数字的指针的 FOR 循环

清单 6.6 展示了 Palindromes1.c 的内容，说明如何判断一个字符串是否为回文。如果你已经忘了，回文是指自身呈“镜像”的数字或字符串，例如 12321、“rotor”和“radar”，而 1231 和“rattan”不是回文。

### 清单 6.6：Palindromes1.c

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

清单 6.6 包含 C 函数 `scanString`，其中的循环从值 0 开始，最终值为 `len /2`，即字符串 `str` 中元素数量的一半。该循环逐步从左向右移动，将当前位置的字符内容与字符串 `line1` 的“另一端”对应字符进行比较。

例如，数字 1234321 会将左侧数字 1 与该数字右侧对应位置的数字（也是 1）进行比较。接下来，左侧数字 2 与右侧数字 2 匹配，然后比较左侧数字 3 与其右侧对应数字。中间数字没有对应位置，这意味着我们已经验证数字 1234321 实际上是一个回文。

按照上一段描述的相同过程，字符串“rotor”和“radar”是回文，但数字 12345321 不是回文（它缺少对应的数字 4）。

编译清单 6.6 中的代码并运行可执行文件 `Palindromes1`，你将看到以下输出：

```text
Current Word: radar
Palindrome: YES
Current Word: motion
Palindrome: NO
```

## 指针、循环与数字的因数

清单 6.7 包含一个 while 循环、条件逻辑以及 %（取模）运算符，用于找出任何大于 1 的整数的因数。

### 清单 6.7：Divisors2.c

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int main()
{
    char *primes, prime[20];
    int div=2, num=12;

    printf("Number: %d\n", num);

    while(num > 1)
    {
        if(num % div == 0)
        {
            // convert number to string
            sprintf(prime, "%d", div);

            // append string to main string
            asprintf(&primes, "%s %s", primes, prime);

            num /= div;
        }
        else
        {
            ++div;
        }
    }

    printf("Divisors: %s\n", primes);

    return 0;
}
```

[清单 6.7](#) 与 [清单 6.6](#) 之间的主要区别在于，前者在 *while 循环* 中构造变量 divList（它是某个数的因数的串联列表），然后在 *while 循环* 完成时返回 divList 的值。[清单 6.7](#) 的输出如下：

```text
Number: 12
Divisors: (null) 2 2 3
```

请记住，`asprintf()` 函数最近才在《动态内存技术报告》中标准化，并不属于 C 标准本身。只有当编译器定义了 `__STDC_ALLOC_LIB__`，并且用户在包含 string.h 之前将 `__STDC_WANT_LIB_EXT2__` 定义为 1 时，此函数才可用。

## 指针与数字数组

清单 6.8 展示了 PointersArrayNums1.c 的内容，说明如何初始化字符串和指针。

### 清单 6.8：PointersArrayNums1.c

```c
#include <stdio.h>

int main()
{
 int numbers[] = {1,2,3,4,5};
 int *ptr1 = numbers;
 int size1 = sizeof(numbers)/sizeof(int);

 for(int i=0; i<size1; i++)
 {
 printf("%d\n", *(ptr1+i));
 }

 //see what happens when you use these invalid lines:
 //for(int ptr1=numbers; ptr1 != NULL; ptr1++)
 //for(int *ptr1=&numbers[0]; *ptr1 != '\0'; ptr1++)
 //for(int *ptr1=&numbers[0]; *ptr1; ptr1++)

 return 0;
}
```

清单 6.8 很直接：main() 函数用五个整数值初始化数组 numbers，然后将指针 ptr1 初始化为 numbers 数组的位置。

main() 方法的下一部分包含一个循环，该循环遍历 numbers 数组中的值并打印这些值。运行清单 6.8 中代码后的输出如下：

```text
1
2
3
4
5
```

## 指针数组

清单 6.9 展示了 `ArrayOfPointers.c` 的内容，说明如何初始化指针数组。

### 清单 6.9：ArrayOfPointers.c

```c
#include <stdio.h>

int main()
{
    int a=100, b=-200, c=500;
    int *p[3];

    p[0]= &a;
    p[1]= &b;
    p[2]= &c;

    printf("Initial a: %d b: %d c: %d\n",*p[0],*p[1],*p[2]);

    *p[0] += 100;
    *p[1] += 200;
    *p[2] += 300;

    printf("Updated a: %d b: %d c: %d\n",*p[0],*p[1],*p[2]);

    return 0;
}
```

**清单 6.9** 分别用值 100、-200 和 500 初始化三个整型变量 a、b 和 c。接下来的代码片段是大小为 3 的指针数组 p 的声明。元素 p[0]、p[1] 和 p[2] 分别用变量 a、b 和 c 的地址初始化。

接下来，位置 p[0]、p[1] 和 p[2] 分别增加 100、200 和 300，然后 printf() 语句显示它们的值。运行清单 6.9 中代码后的输出如下：

```text
Initial a: 100 b: -200 c: 500
Updated a: 200 b: 0 c: 800
```

## 指针与函数

本节包含一个示例，说明如何将基于指针的变量传递给函数以修改变量的值。请注意，本章后面会展示一个指向函数的指针的示例（它不同于本节中的概念）。

清单 6.10 展示了 PointersAndFunctions1.c 的内容，说明如何初始化字符串和指针。

### 清单 6.10：PointersAndFunctions1.c

```c
#include <stdio.h>

void test(int *num)
{
    *num += 6;
    printf("num inside test: %d\n", *num);
}

int main()
{
    int num = 7;

    printf("num before test: %d\n", num);

    test(&num);

    printf("num after test: %d\n", num);

    return 0;
}
```

[清单 6.10](#) 包含函数 `test()`，该函数将其基于指针的参数增加 6，然后显示新值。`main()` 函数用值 7 初始化变量 `num`，然后在调用函数 `test()` 之前和之后分别显示 `num` 的值。运行 [清单 6.10](#) 中代码后的输出如下：

```text
num before test: 7
num inside test: 13
num after test: 13
```

## 指针与小数数组

[清单 6.11](#) 展示了 PointersDecimals1.c 的内容，说明如何初始化字符串和指针。

### 清单 6.11：PointersDecimals1.c

```c
#include <stdio.h>

int main()
{
    int ints1[] = {1.0,2.0,3.0,4.0,5.0};
    int *ptr1 = ints1;
    int isize1 = sizeof(ints1)/sizeof(int);
```
