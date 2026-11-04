
```c
{
    test(3, "text_1", "text_2", "text_3");
    return 0;
}

void test(int num, ...)
{
    char *str;
    int i;
    va_list arg_ptr;

    va_start(arg_ptr, num); /* arg_ptr points to the first optional
argument. Notice that the name of the second argument should be the same
with the name of the last fixed parameter in the definition of test(). */

    for(i = 0; i < num; i++)
    {
        str = va_arg(arg_ptr, char*); /* Each call of va_arg()
returns the value of the respective optional argument of type char* and
arg_ptr advances to point to the next optional argument. The second
argument is char*, because it is said that the type of all optional
arguments is char*. */
        printf("%s ", str);
    }
    va_end(arg_ptr);
}
```

程序输出可选参数的值：text_1 text_2 text_3。使用带有可变参数列表的函数的首要困难在于，没有简单的方法来确定其可选参数的数量和类型。为了确定数量，一个简单的解决方案是添加一个固定参数，由它声明该数量。在前面的示例中，我们使用了参数 num。如果所有参数都是同一类型，我们可以使用一个特殊值来标记列表的结尾。此外，必须以某种方式告知函数这些参数的类型。例如，printf() 和 scanf() 使用格式字符串来获取处理参数列表所需的类型信息。

## 练习

`C.11.45` 编写一个函数，接受一个 `double` 类型的可变参数列表并返回最大值。编写一个程序，读取三个浮点数并使用该函数显示最大值。

```c
#include <stdio.h>
#include <stdlib.h>

double find_max(int num, ...);

int main(void)
{
    double i, j, k;

    printf("Enter numbers: ");
    scanf("%lf%lf%lf", &i, &j, &k);

    printf("Max = %f\n", find_max(3, i, j, k));
    return 0;
}

double find_max(int num, ...)
{
    int i;
    double max, tmp;
    va_list arg_ptr;

    va_start(arg_ptr, num);
    max = va_arg(arg_ptr, double);
    for(i = 1; i < num; i++)
    {
        tmp = va_arg(arg_ptr, double);
        if (max < tmp)
            max = tmp;
    }
    va_end(arg_ptr);
    return max;
}
```

注释：请注意，find_max() 可用于求任意数量 double 参数的最大值，而不仅仅是 3 个。

## 递归函数

调用自身的函数称为递归函数。例如：

```c
#include <stdio.h>

void show(int num);

int main(void)
{
    int i;

    printf("Enter number: ");
    scanf("%d", &i);

    show(i);
    return 0;
}
```

```c
void show(int num)
{
    if(num > 1)
        show(num-1);
    printf("val = %d\n", num);
}
```

为了了解递归如何工作，假设用户输入一个大于 1 的数，例如 3，从而再次调用 show()。

- a. 在 show() 的第一次调用中，由于 num = 3 > 1，show() 以参数 num-1 = 3-1 = 2 调用自身。printf() 未被执行。由于 show() 尚未终止，为值为 3 的变量 num 分配的内存以及与函数调用相关的其他信息不会被释放。
- b. 在 show() 的第二次调用中，为 num 变量分配了新的内存。由于 num = 2 > 1，show() 再次以参数 num-1 = 2-1 = 1 调用自身。与之前一样，printf() 未被执行，为值为 2 的新变量 num 分配的内存不会被释放。
- c. 与之前一样，在 show() 的第三次调用中，为 num 变量分配了新的内存。由于 num 不大于 1，show() 不再被调用。因此，这个 printf() 被执行并输出 val = 1。为该 num 分配的内存被释放。

接下来，所有未执行的 printf() 将按顺序执行，从最后一个开始。在 show() 的每次终止时，为相应的 num 以及每次特定调用分配的内存都会被释放。因此，程序显示：

```
val = 1
val = 2
val = 3
```

> 递归函数必须包含终止条件，以防止无限递归。

在我们的示例中，这个条件是语句 if(num > 1)。

每次递归函数调用自身时，都会从栈中分配新内存来存储其自动变量。在我们的示例中，创建了三个不同的 num 变量，每个具有不同的值。描述这一点的一种简单方式是，把每个 num 看作叠放在另一个之上（例如，一摞脏盘子），在递归结束时，我们访问最后创建的那个 num（例如，取走这摞盘子顶部的盘子）。对于静态变量，不会分配新内存；也就是说，所有函数调用共享相同的静态变量。关于代码的哪一部分尚未执行的信息也存储在栈中。当函数不再调用自身时，该代码将反向执行。

在我们的示例中，每个 num 的值存储在栈中，每个 printf() 将按照与函数调用相反的顺序执行，即从最后一个到第一个。一旦 show() 不再调用自身，即当 num 变为 1 时，就会发生这种情况。

然而，栈的大小可能不足以存储与每次函数调用相关的信息。例如，如果用户输入一个很大的值，比如 100000，程序执行可能会终止，并出现消息“Stack overflow”，这表明栈中没有其他可用内存。栈的默认大小取决于具体实现，不过编译器通常提供更改它的能力。

在实践中，递归常用于实现数学算法或数据结构中的操作。例如，我们将在第 14 章中使用递归来实现二叉搜索树中的几个函数。然而，如果你能编写等效的代码，那可能是个更好的主意。例如，改用迭代循环。尽管递归代码可能更易于阅读和编写，但循环的性能可能会更好。

## 练习题

### C.11.46 以下程序的输出是什么？

```c
#include <stdio.h>

int a = 4;

int main(void)
{
    if(a == 0)
        return 0;
    else
    {
        printf("%d ", a--);
        main();
    }
    return 0;
}
```

答案：请注意，main() 也可以被递归调用。在每次调用中，a 递减 1。一旦 a 变为 0，程序就停止调用 main()。因此，程序显示：4 3 2 1

### C.11.47 以下程序的输出是什么？

```c
#include <stdio.h>

int unknown(int arr[], int num);

int main(void)
{
    int arr[] = {10, 20, 30, 40};
    printf("%d\n", unknown(arr, 4));
    return 0;
}
```

```c
int unknown(int arr[], int num)
{
    if(num == 1)
        return arr[0];
    else
        return arr[num-1] + unknown(arr, num-1);
}
```

答案：当调用 unknown() 时，它返回

arr[4-1 = 3] + unknown(arr, 4-1 = 3) =
arr[3] + (arr[3-1] + unknown(arr, 3-1)) =
arr[3] + arr[2] + (arr[2-1] + unknown(arr, 2-1)) =
arr[3] + arr[2] + arr[1] + unknown(arr, 1)

最后一次调用 unknown(arr, 1) 返回 arr[0]，因为 num = 1。因此，返回值为 arr[3]+arr[2]+arr[1]+arr[0]，程序输出 100。结果，该函数递归计算数组元素之和。

### C.11.48 编写一个递归函数，接受整数 n 作为参数并返回其阶乘，使用公式 n! = n×(n-1)!。整数 n（其中 n >= 1）的阶乘是从 1 到 n 的整数的乘积，即 1×2×3×...×n。0 的阶乘是 1（0!=1）。编写一个程序，读取一个小于 170 的正整数，并使用该函数显示其阶乘。

```c
#include <stdio.h>

double fact(int num);

int main(void)
{
    int num;
    do
    {
        printf("Enter a positive integer less than 170: ");
        scanf("%d", &num);
    } while(num < 0 || num > 170);

    printf("Factorial of %d is %e\n", num, fact(num));
    return 0;
}

double fact(int num)
{
    if((num == 0) || (num == 1))
        return 1;
    else
        return num * fact(num-1);
}
```
