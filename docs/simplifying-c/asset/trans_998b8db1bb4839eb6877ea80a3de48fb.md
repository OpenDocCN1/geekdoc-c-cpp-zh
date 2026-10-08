
Q8. 编写一个程序，使用递归函数 fact 来求给定数字 N 的阶乘。

Q9. 编写一个程序，使用一个函数返回序列 1,3,5,7 中的下一个元素。使用静态变量。

Q10. 编写一个程序，对从命令行传递过来的数值数据进行排序。

Q11. 编写一个程序，找出通过命令行传递的数据中的最大数。

Q12. 编写一个程序，计算通过命令行传递的数的平均值。

## 09 数组

### 目标

- 什么是数组
- 描述数组的维度

在前面的章节中，我们学习了如何在 C 语言中使用基本数据类型，如 int、char、float 等。这些数据类型被用于定义单个变量。有时，单个变量无法满足我们的需求。例如，假设我们需要计算一个班 30 名学生的成绩。如果使用基本数据类型，我们需要 30 个不同的变量。同时管理 30 个不同的变量始终是一个问题。C 语言提供了派生数据类型的概念来解决这个问题。在本章中，我们将讨论一种称为数组的派生数据类型。我们还将学习如何从数组中存储和检索数据以及数组的应用。
让我们首先讨论什么是数组。

### 9.1 什么是数组

如前所述，管理独立的变量始终是一个问题。C 语言允许我们使用现有的基本数据类型创建数据结构。这种数据结构可以很容易地管理。数组就是这样一种数据结构。数组被定义为具有相同数据类型、在内存中一个接一个存储的元素序列，并通过共同的名字引用。图 1 展示了数组变量以及其他变量的内存表示：

![](img/5d422ba7108ffdf64376be51eaf0c459_198_0.png)

从图 1 中可以看出，一组变量构成了一个被标识为 Marks 的块。由于元素按顺序一个接一个地存储，这种内存分配被称为连续内存分配。这里的 Marks 代表一个具有七个元素的数组。每个元素都具有相同的数据类型。

由于整个块通过名称 *Marks* 引用，C 编译器需要一种机制来标识该块内的各个元素。为了标识块中的每个元素，使用索引值。C 语言中的索引值从零开始。因此，数组 Marks 的元素被标识为 Marks[0]、Marks[1]、Marks[2]、Marks[3]、Marks[4]、Marks[5] 和 Marks[6]。这些元素中的每一个都独立地作为一个单一变量工作。可以在普通变量上执行的所有操作也可以在数组元素上执行。图 2 表示了数组的修改后的内存表示：

![](img/5d422ba7108ffdf64376be51eaf0c459_199_0.png)

从图 2 中可以看出，单独的数组元素现在有了诸如 Marks[0]、Marks[1] 等名称。使用的索引是整数或结果为整数的表达式。不允许使用其他索引值。当数组名称在没有索引的情况下使用时，指的是数组第一个元素的地址。换句话说，它指的是数组的起始地址。

还可以观察到，图 2 中显示的内存块看起来像是一个有一行一列的表格。C 允许我们拥有不同维度的数组。下一节讨论数组的维度。

### 9.2 数组的维度

C 将数组分类为一维数组和多维数组。一维数组有一行，而多维数组有多行和多列。多维数组中的行数和列数由用户指定。现在让我们讨论如何定义和使用一维数组。

- **一维数组**
我们知道，数组用于将多个相同数据类型的变量分组在单个名称之下。声明一维数组的语法如下：

`data type identifier[size];`

数据类型标识了存储在数组中的数据类型的类型；它可以是整型、浮点型、字符型、双精度型或任何基本数据类型。标识符指的是数组的名称，而大小指示可以存储在数组中的最大元素数量。
例如，`float f_marks[10];` 定义变量 f_marks 为一个数组，该数组能够存储 10 个浮点值。

数组一旦定义，可以在编译时或运行时初始化。在编译时初始化中，值在数组声明时分配。在运行时初始化中，用户在程序执行期间输入值。在编译时初始化数组的语法如下：

```
data type identifier[size] = { value 1, value 2, ......., value n };
or
data type identifier [ ] = { value 1, value 2, ......., value n };
```

如果在编译时分配值，数组的大小是可选的。在这种情况下，编译器将根据指定的值数量自动为数组分配大小。程序 1 说明了数组的使用和编译时初始化：

▶ **程序 1**

```c
/* Program to illustrate the use of array */
#include<stdio.h>
/* Beginning of main function */
main()
{
/* Declare variables */
int i_ctr;
float f_marks[10]={55.75,50.25,75.55,65,75.85};
/* Print the values in array */
printf("Elements of array\n");
for(i_ctr = 0; i_ctr < 10; i_ctr++)
printf("\nValue of element number %d is %.2f\n",i_ctr+1,f_marks[i_ctr]);
return;
}
/* End of function main */
```

**输出：**

```
Elements of array
Value of element number 1 is 55.75
Value of element number 2 is 50.25
Value of element number 3 is 75.55
Value of element number 4 is 65.00
Value of element number 5 is 75.85
Value of element number 6 is 0.00
Value of element number 7 is 0.00
Value of element number 8 is 0.00
Value of element number 9 is 0.00
Value of element number 10 is 0.00
```

在程序 1 中，我们定义了大小为 10 的数组。在初始化时，我们只指定了五个值。因此，编译器将值分配给前五个元素，其余的值被初始化为零。图 3 展示了数组 f_marks 的内存表示：

![](img/5d422ba7108ffdf64376be51eaf0c459_201_0.png)

▲ **图 3：数组 f_marks 的内存表示**

从图 3 中可以观察到，数组的每个元素占用 4 字节的内存。那么数组占据的总内存可通过数组大小乘以数据类型大小得出。在上面的情况下，数组的大小是 10，float 的大小是 4，因此占据的总内存为 10 × 4 = 40 字节。

尽管允许数组的编译时初始化，但很少使用。大多数程序员更喜欢数组的运行时初始化。数组值像任何普通变量一样读取。读取时唯一的区别在于索引的使用。程序 2 说明了数组运行时初始化的使用：

▶ **程序 2**

```c
/* Program to illustrate the use of array */

#include<stdio.h>
#define MAX 25

/* Beginning of main function */
main()
{
   /* Declare variables */
   int i_ctrl, i_num;
   int i_array[MAX];

   /* Read Data */
   printf("Number of elements in array: ");
   scanf("%d",&i_num);

   for(i_ctrl = 0; i_ctrl < i_num ; i_ctrl++)
   {
      printf("\nElement %d: ",i_ctrl + 1);
      scanf("%d",&i_array[i_ctrl]);
   }

   /* Print Data */
   for(i_ctrl = 0; i_ctrl < i_num ; i_ctrl++)
   printf("Value of element number %d is %d\n",i_ctrl+1,i_array[i_ctrl]);
   return;
}
/* End of function main */
```

**输出：**

```text
Number of elements in array: 5

Element 1: 55
Element 2: 27
Element 3: -19
Element 4: 39
Element 5: 12

Value of element number 1 is 55
Value of element number 2 is 27
Value of element number 3 is -19
Value of element number 4 is 39
Value of element number 5 is 12
```

在程序 2 中，我们定义了大小为 25 的数组。当输入数据时，我们只使用了其中的五个。这在大多数应用中是正常情况。此外，C 编译器不检查数组边界。边界需要由程序员处理。例如，如果程序员定义了大小为 5 的数组，而用户向其中读取了 10 个值，在这种情况下，编译器仅会在编译时初始化时生成错误。然而，对于运行时初始化，它不会生成任何错误。在这种情况下，用户需要小心，因为读取额外元素可能会覆盖程序的合法变量。程序 3 说明了数组边界的示例：

▶ **程序 3**

```c
/* Program to illustrate the use of array */

#include<stdio.h>
#define MAX 5

/* Beginning of main function */
main()
{
   /* Declare variables */
   int i_ctr;
   int i_array[MAX];

   /* Read data */
   printf("Enter values\n");
   for(i_ctr = 0; i_ctr < 10 ; i_ctr++)
   {
      printf("\nElement %d", i_ctr + 1);
      scanf("%d",&i_array[i_ctr]);
   }

   /* Print Data */
   printf("Array Elements\n");
   for(i_ctr = 0; i_ctr < 10 ; i_ctr++)
   printf("\nValue of element number %d is %d\n",i_ctr+1,i_array[i_ctr]);
}
```

