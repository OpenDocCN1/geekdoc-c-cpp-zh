
使用 C 和 C++ 编程

```
checkPrimeNumber();    // 没有传递参数
return 0;
}
// 返回类型为 void，意味着不返回任何值
void checkPrimeNumber()
{
    int n, i, flag = 0;
    printf("Enter a positive integer: ");
    scanf("%d",&n);
    for(i=2; i<= n/2; ++i) {
        if(n%i == 0) {
            flag = 1;
        }
    }
    if (flag == 1)
        printf("%d is not a prime number.", n);
    else
        printf("%d is a prime number.", n);
}
```

`checkPrimeNumber()` 函数从用户获取输入，检查其是否为质数并显示在屏幕上。
`main()` 函数内部 `checkPrimeNumber();` 语句中的空括号表示没有向函数传递参数。
函数的返回类型为 `void`。因此，函数没有返回任何值。

示例 2：未传递参数但有返回值：

```c
#include<stdio.h>
int getInteger();

int main()
{
    int n, i, flag = 0;

    // 没有传递参数
    n = getInteger();

    for(i=2; i<=n/2; ++i)
    {
        if(n%i==0){
            flag = 1;
            break;
        }
    }

    if (flag == 1)
        printf("%d is not a prime number.", n);
    else
        printf("%d is a prime number.", n);

    return 0;
}

// 返回用户输入的整数
getInteger()
{
    int n;

    printf("Enter a positive integer: ");
    scanf("%d",&n);

    return n;
}
```

`n = getInteger();` 语句中的空括号表示没有向函数传递参数。并且，函数返回的值被赋值给 `n`。

在这里，`getInteger()` 函数从用户处获取输入并返回。检查数字是否为质数的代码位于 `main()` 函数中。

## 示例 3：传递了参数但没有返回值：

```c
#include <stdio.h>
void checkPrimeAndDisplay(int n);
int main()
{
    int n;

    printf("Enter a positive integer: ");
    scanf("%d",&n);

    // n 被传递给函数
    checkPrimeAndDisplay(n);

    return 0;
}

// 返回类型为 void，意味着不返回任何值
void checkPrimeAndDisplay(int n)
{
    int i, flag = 0;
    for(i=2; i<= n/2; ++i)
    {
        if(n%i == 0){
            flag = 1;
            break;
        }
    }
    if(flag == 1)
        printf("%d is not a prime number.",n);
    else
        printf("%d is a prime number.", n);
}
```

用户输入的整数值被传递给 `checkPrimeAndDisplay()` 函数。

在这里，`checkPrimeAndDisplay()` 函数检查传递的参数是否为质数并显示相应的消息。

## 示例 4：传递了参数且返回值：

```c
#include <stdio.h>
int checkPrimeNumber(int n);

int main()
{
    int n, flag;

    printf("Enter a positive integer: ");
    scanf("%d",&n);

    // n 被传递给 checkPrimeNumber() 函数
    // 返回值被赋值给 flag 变量
    flag = checkPrimeNumber(n);

    if(flag == 1)
        printf("%d is not a prime number",n);
    else
        printf("%d is a prime number",n);

    return 0;
}

// 从函数返回 int 类型
int checkPrimeNumber(int n)
{
    int i;
    for(i=2; i<= n/2; ++i)
    {
      if(n%i == 0)
        return 1;
    }

    return 0;
}
```

来自用户的输入被传递给 `checkPrimeNumber()` 函数。`checkPrimeNumber()` 函数检查传递的参数是否为质数。

如果传递的参数是质数，函数返回 0。如果传递的参数不是质数，函数返回 1。返回值被赋值给 `flag` 变量。

取决于 `flag` 是 0 还是 1，`main()` 函数会打印相应的消息。

## C 语言中的递归函数

调用它自身的函数被称为递归函数。这种技术被称为递归。

## 递归是如何工作的？

```c
void recurse()
{
  ...
  ...
  recurse();
  ...
  ...
}

int main()
{
  ...
  ...
  recurse();
  ...
  ...
}
```

## 递归是如何工作的？

```c
void recurse() {
    ... ... ...
    recurse(); // 递归调用
    ... ... ...
}

int main() {
    ... ... ...
    recurse();
    ... ... ...
}
```

递归会持续进行，直到满足某个防止它的条件。
为了防止无限递归，可以使用 `if...else` 语句（或类似的方法），其中一个分支将停止递归。

## 递归示例

使用递归计算自然数的和：

```c
#include <stdio.h>

int main() {
    int n, result;

    printf("Enter a positive integer: ");
    scanf("%d",&n);

    result = sum(n);
    printf("sum = %d\n", result);

    return 0;
}

int sum(int n) {
    if (n != 0)
        // sum() 调用自身
        return n + sum(n-1);
    else
        return n;
}
```

**输出：**
Enter a positive integer: 3
sum = 6

初始情况下，`sum()` 被 `main()` 函数调用。在下一次调用中，传递了 `2`。这个过程持续到 `n` 等于 0。

## 递归的优点和缺点

- 递归使代码优雅。
- 递归通常用于阶乘、斐波那契、塔霍塔和树遍历等问题。
- 然而，递归比迭代慢。
- 每次递归调用都会消耗栈内存。

## 数组

数组是相同类型固定大小的数据结构。

## C 数组的特性

1. 数组元素具有相同的数据类型。
2. 数组元素存储在连续的位置。
3. 数组名代表起始元素的地址。
4. 声明时应注明数组大小。

## 一维数组

### 数组声明

在 C 中中声明数组时，程序员指定元素的类型和数组所需的元素数量如下：

```c
type arrayName[arraySize];
```

这被称为一维数组。`arraySize` 必须是大于零的整数。例如，要声明一个名为 `balance` 的双精度类型数组，使用此语句：

```c
double balance[10];
```

### 数组初始化

可以通过以下方式初始化数组：

```c
double balance[5]={1000.0,2.0,3.4,7.0,50.0};
```

大括号 `{}` 之间的数值不能大于方括号 `[]` 中声明的元素数量。

如果你省略数组的大小，将创建一个足够容纳初始化的数组。如果写：

```c
double balance[]={1000.0,2.0,3.4,7.0,50.0};
```

你创建一个与上一个示例完全相同的数组。以下是赋值单个元素的示例：

```c
balance[4]=50.0;
```

上述语句将数组的第 5 个元素赋值为 50.0。所有数组都以 0 作为第一个元素的索引（也称为基索引），数组的最后一个索引将是总大小减 1。下面是我们讨论的数组的图示表示：

| 0 | 1 | 2 | 3 | 4 |
|---|---|---|---|---||
| balance | 1000.0 | 2.0 | 3.4 | 7.0 | 50.0 |
