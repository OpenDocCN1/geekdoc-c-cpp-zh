

# 程序 - 指针变量中的星号与操作符地址

```c
#include <stdio.h>
#include <string.h>

int main() {
{
    int i = 5;
    int *ptr;
    ptr = &i;

    printf("Address of i = %u\n", i);
    printf("Address of ptr = %u\n", &ptr);
    printf("Address of i = %u\n", *ptr);
    return 0;
}
```

Output:
Address of i = 65522
Address of ptr = 65526
Address of i = 65522

> 注意：在上述程序中，第三个 printf 有意义。简单来说，星号 (*) 和地址 (&) 运算符相互抵消了。

# 空指针 (NULL POINTER)

在没有确切地址可以赋值时，为指针变量赋值 NULL 值始终是一个良好的习惯。这在变量声明时完成。赋值为 NULL 的指针称为空指针。

NULL 指针是在几个标准库中定义的值为零的常量。考虑以下程序。

# 指针、结构体与联合体

```c
#include<stdio.h>
int main(){
int*ptr = NULL;
printf("The value of the ptr is : %x\n", ptr );
return 0;
}
```

当上述代码被编译并执行时，会产生以下结果：

The value of ptr is 0

# C语言中使用指针时的常见错误

以下是程序员在处理指针时通常容易犯的一些错误：

# 1. 指针的类型类型错误

需要说明的是，为了避免数据丢失，为指针分配正确的数据类型非常重要。

例如，如果指针的数据类型是整数类型，C 编译器会认为指针将指向的变量地址将存储整数值，因此在谈论 64 位编译器时，编译器会为其预留 4 字节的空间。

让我们考虑这段代码片段：

```c
/* 这里，变量 number1 和 number2 都是 long 类型，
   占用 8 字节 */ / long number1, number2; int *p;
scanf("%d",&number1); // 以 long 数据类型输入 number1 的值
p = &number1; // 将 number1 的地址存储到指针 p 中
number2 = // 将 p 指向的值存储到 number2
```

# 2. 错误的初始化

我们倾向于混淆变量的值及其内存地址。假设我们有一个 `int` 类型的变量 'a' 和另一个 `int` 类型的指针 *p*，那么以下初始化是错误的：

```c
a = p;
*p = &a;
```

必须理解的是这是错误的，因为 'a' 是一个变量，而 p 是它的内存地址。

# 指针的算术运算（C 中的指针算术）

C 允许像你这样的程序员使用指针进行算术运算。因此，程序员可以使用指针变量执行任何算术运算。使用指针变量进行算术运算被称为指针算术操作。

我们可以对指针进行加、减等算术运算，但正如所知，指针包含地址，如果另一个操作数是整数类型，那么对指针执行的算术运算的结果也将是一个指针。在指针减指针减法中，结果将是一个整数值。

在 C 语言中，指针可以执行以下算术运算：

* *递增 (Increment)*
- *递减 (Decrement)*
- *加法 (Addition)*
- *减法 (Subtraction)*
- *比较 (Comparison)*

# 递增指针变量

如果将指针加 1，指针将开始指向下一个位置。这与通用算术有所不同，因为指针的增加量取决于它所指向的数据类型的大小。

我们可以使用对指针的递增操作来遍历数组，指针将一直指向数组的每个元素，对其执行某些操作并在循环中更新它。

递增指针的规则如下：

```c
new_address = current_address + i * size_of(data_type)
```

其中 i 是指针增加的倍数。

# 32 位

对于 32 位 int 变量，它将增加 2 字节。

# 64 位

对于 64 位 int 变量，它将增加 4 字节。

让我们看看在 64 位架构上递增指针变量的示例。

```c
#include<stdio.h>
int main(){
 int number=50;
 int *p;//指向 int 的指针
p=&number;//存储 number 变量的地址
printf("Address of p variable is %u \n",p);
p=p+1;

printf("After increment: Address of p variable is %u \n",p); // 在我们的情况下，
 p 将增加 4 字节。
 return 0;
}
```

Output:
Address of p variable is 3214864300
After increment: Address of p variable is 3214864304

# 使用指针遍历数组

```c
#include<stdio.h>
void main ()
{
 int arr[5] = {1, 2, 3, 4, 5};
 int *p = arr;
 int i;

printf("printing array elements...\n");
for(i = 0; i < 5; i++)
{
 printf("%d ",*(p+i));
}
```

Output:
printing array elements...
1 2 3 4 5

# C 中的指针递减

与加法类似，我们可以对指针进行递减操作。如果我们递减一个指针，它将指向前一个位置。递减指针的规则如下：

```c
new_address = current_address - i * size_of(data_type)
```

32 位
对于 32 位 int 变量，它将减少 2 字节。

64 位
对于 64 位 int 变量，它将减少 4 字节。

让我们看看在 64 位架构上递减指针变量的示例。

```c
#include<stdio.h>
int main(){
 int number=50;
 int *p;//指向 int 的指针
p=&number;//存储 number 变量的地址
printf("Address of p variable is %u \n",p);
p=p-1;

printf("After decrement: Address of p variable is %u \n",p); // 在我们的情况下，
 p 将减少 4 字节。
 return 0;
}
```

Output:
Address of p variable is 3214864300
After decrement: Address of p variable is 3214864296

# C 中的指针加法

我们可以对指针变量执行加法运算。对指针加法任何数字将得到一个地址。对指针加法的公式如下：

```c
new_address = current_address + i * size_of(data_type)
```

32 位
对于 32 位 int 变量，它将增加 2 * 字节。

64 位
对于 64 位 int 变量，它将增加 4 * 字节。

让我们看看在 64 位架构上对指针变量加法的示例。

```c
#include<stdio.h>
int main(){
 int number=50;
 int *p;//指向 int 的指针
p=&number;//存储 number 变量的地址
printf("Address of p variable is %u \n",p);
p=p+1;

printf("After increment: Address of p variable is %u \n",p); // p 将增加 4 字节
 return 0;
}
```

Output:
Address of p variable is 3214864300
After increment: Address of p variable is 3214864304

# C 中的指针减法

与指针加法类似，我们可以对指针变量执行减法运算。从指针中减去任何数字将得到一个地址。对指针减法的公式如下：

```c
new_address = current_address - i * size_of(data_type)
```

32 位
对于 32 位 int 变量，它将减少 2 * 字节。

64 位
对于 64 位 int，它将减少 4 * 字节。

让我们看看在 64 位架构上对指针变量减法的示例。

```c
#include<stdio.h>
int main(){
 int number=50;
 int *p;//指向 int 的指针
p=&number;//存储 number 变量的地址
printf("Address of p variable is %u \n",p);
p=p-3; // 从指针中减去 3
printf("After subtracting 3: Address of p variable is %u \n",p);
 return 0;
}
```

Output:
Address of p variable is 3214864300
After subtracting 3: Address of p variable is 3214864288

