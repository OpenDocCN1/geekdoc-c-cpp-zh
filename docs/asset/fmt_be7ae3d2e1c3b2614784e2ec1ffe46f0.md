
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

在程序 2 中，我们定义了大小为 `25` 的数组。当输入数据时，我们只使用了其中的五个。这在大多数应用中是正常情况。此外，C 编译器不检查数组边界。边界需要由程序员处理。例如，如果程序员定义了大小为 `5` 的数组，而用户向其中读取了 `10` 个值，在这种情况下，编译器仅会在编译时初始化时生成错误。然而，对于运行时初始化，它不会生成任何错误。在这种情况下，用户需要小心，因为读取额外元素可能会覆盖程序的合法变量。程序 3 说明了数组边界的示例：

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

# C 语言编程：数组

#### 程序 3

```c
return;
}
/* End of function main */
```

**输出：**

- 输入数值：
  - 元素 1：45
  - 元素 2：57
  - 元素 3：23
  - 元素 4：45
  - 元素 5：90
  - 元素 6：85
  - 元素 7：34
  - 元素 8：32
  - 元素 9：67
  - 元素 10：45

**数组元素**

- 第 1 个元素的值为 45
- 第 2 个元素的值为 57
- 第 3 个元素的值为 23
- 第 4 个元素的值为 45
- 第 5 个元素的值为 90
- 第 6 个元素的值为 85
- 第 7 个元素的值为 34
- 第 8 个元素的值为 32
- 第 9 个元素的值为 67
- 第 10 个元素的值为 45

在程序 3 中，我们定义了一个大小为五的数组。用于读取数据的循环迭代了 `10` 次，因此，我们不仅读取了 `5` 个值，而是能够读取 `10` 个值。编译器允许我们读取 `10` 个值，这是由于数组内存连续性的特性。数组的这一特性有时可能会引发问题。让我们试着理解它如何在数组的第六个位置存储值。

如前所述，数组的名称指向第一个元素的地址。编译器使用第一个地址作为基准来计算其余的地址。计算任意元素地址的公式如下：

> 索引 `I` 处的元素地址 = 数组基准地址 + (`数据类型大小` × 索引 `I`)

例如，如果一个浮点数数组起始于地址 `655208`，我们需要找到索引 `3` 处元素的起始地址，则上述公式可以写为：

```
索引 3 处的元素地址 = 655208 + (4 × 3)
= 655208 + 12
= 655220
```

可以通过图 3 中显示的元素的地址进行交叉验证。该等式对任意索引都成立。因此，即使我们只定义了数组中的五个元素，编译器也会使用上述公式计算任意索引的地址并在那里存储一个值。

一旦赋值，数组元素就可以像普通变量一样使用。我们可以对数组元素执行赋值、比较等操作。程序 4 说明了如何从给定数组中查找最大值：

#### 程序 4

```c
/* Program to find the maximum value from an array */  
#include<stdio.h>  
#define MAX 5  
  
/* Function to find maximum value */  
int findmax(int *temp)  
{  
   int i_ctr;  
   /* Initialize first element of array to maximum */  
   int i_max = temp[0];  
   
   /* Compare with other elements in array */  
   for(i_ctr = 1; i_ctr < MAX; i_ctr++)  
   {  
        if(temp[i_ctr] > i_max)  
            i_max = temp[i_ctr];  
   }  
   return i_max;  
}  
/* End of function */  
   
/* Beginning of main function */  
main()  
{  
   /* Declare variables */  
   int i_ctr, i_max;  
   int i_array[MAX];  
   
   /* Read Data */  
   
   for(i_ctr = 0; i_ctr < MAX; i_ctr++)  
   {  
        printf("\nElement %d: ",i_ctr + 1);  
        scanf("%d",&i_array[i_ctr]);  
   }  
   
   i_max = findmax(i_array);  
   /* Print Data */  
   printf("\nThe maximum value in the array is %d\n",i_max);  
   return;  
}  
/* End of function main */
```

**输出：**

```
Element 1: 25  
Element 2: 35  
Element 3: 10  
Element 4: 99  
Element 5: 5  
   
The maximum value in the array is 99
```

在程序 4 中，我们定义了两个函数，即 `main` 和 `findmax`。`main` 函数接受数组元素并将其传递给 `findmax` 函数。`findmax` 函数接受数组的地址并返回一个整数值。我们观察到 `findmax` 函数中使用了 `int *temp`，其中 `temp` 代表可以存储整型变量地址的指针。由于 `main` 函数中定义的数组是整型，指针 `temp` 接受了数组第一个元素的地址，然后它本身开始像数组一样工作。所有值都是通过使用上述地址公式获得的。

让我们再举一个例子，看看单维数组是如何工作的。程序 5 将输入的数字按值降序排序：

#### 程序 5

```c
/* Program to sort an array */

#include <stdio.h>
#define MAX 5
/* Function sort */
void sort(int *temp)
{
    int i_temp,i_ictlr,i_jctr;

    for(i_ictlr = 0; i_ictlr < MAX-1; i_ictlr++)
    for(i_jctr = i_ictlr + 1; i_jctr < MAX; i_jctr++)
    {
        if(temp[i_ictlr] <= temp[i_jctr])
        {
            i_temp = temp[i_ictlr];
            temp[i_ictlr] = temp[i_jctr];
            temp[i_jctr] = i_temp;
        }
    }
}
/* End of function sort */

/* Beginning of main function */
main()
{
    /* Declare variables */
    int i_ctr;
    int i_array[MAX];

    /* Read Data */
    for(i_ctr = 0; i_ctr < MAX; i_ctr++)
    {
        printf("\nElement %d: ",i_ctr + 1);
        scanf("%d",&i_array[i_ctr]);
    }

    /* Function Call */
    sort(i_array);

    /* Print Data */
    printf("Sorted Array\n");
    for(i_ctr = 0; i_ctr < MAX; i_ctr++)
```

```c
printf("%d\n",i_array[i_ctr]);
return;
}
/* End of function main */
```

**输出：**

- 元素 1：25
- 元素 2：75
- 元素 3：55
- 元素 4：95
- 元素 5：65

排序后的数组

- 95
- 75
- 65
- 55
- 25

在程序 5 中，我们可以交换、比较、赋值和等同数组变量。单维数组有其局限性。例如，假设我们需要存储 20 名学生在两门科目中的成绩。我们可以选择定义两个数组；然而，管理它们又将成为一个问题。多维数组解决了这个问题。下一节讨论如何使用多维数组。

#### 多维数组

我们使用的大多数数据都以多个维度表示。例如，考虑表 1 中给出的数据：

**表 1：示例数据**

| 学号 | 英语 | 数学 | 科学 | 绘画 |
| :------- | :------ | :--- | :------ | :------ |
| 1        | 75      | 90   | 40      | 40      |
| 2        | 50      | 60   | 70      | 85      |
| 3        | 80      | 85   | 55      | 60      |

从表 1 中可以观察到，数据显示了学号 1、2 和 3 在英语、数学、科学和绘画中的得分。这里的数据以多个维度表示，因为我们有三个行和四个列。表 1 中列出的数据可以很容易地使用二维数组在 C 中表示。如果假设所获得的成绩为整数，则多维数组的语法可以声明如下：

```c
int i_mark[行大小][列大小];
```

在上面的语法中，行大小指的是学生的学号，列大小指的是不同的科目。这两个值都是整数值。实体 `i_mark[0][3]` 则指学号 1 在绘画科目中获得的分数。图 4 显示了多维数组的内存表示：

![](img/5d422ba7108ffdf64376be51eaf0c459_207_0.png)

**图 4：多维数组的内存表示**

从图 4 中可以观察到，多维数组在内存中可以用两种不同的方式存储。元素的分配可以按行优先或列优先的方式进行。在这两种情况下，元素的地址将保持不变。获取给定索引的正确值的工作将由编译器完成。定义多维数组的一般语法如下：

```c
数据类型 标识符[大小 1]...[大小 n];
```

上述语法可以根据程序的需要进行修改。在正常情况下，我们可能不需要多于三维的数组。之前定义的数组 `I_mark` 被称为二维数组，因为它有一行和一列。

类似于单维数组，二维数组也可以在编译时进行初始化。在编译时初始化二维数组的语法如下：

```c
数据类型 标识符[行大小][列大小] = { 值 1, 值 2, ..., 值 n };
```

例如，数组 `int I_mark[3][4];` 可以在编译时初始化，如下所示：

```c
int i_mark[2][3] = {75, 90, 40, 40, 50, 60, 70, 85, 80, 85, 55, 60};
```

或

```c
int i_mark[2][3] = {{75, 90, 40, 40},{50, 60, 70, 85},{80, 85, 55, 60}};
```

现在让我们看看如何在 C 中使用多维数组。假设老师希望生成她班上学生的成绩单。程序 6 说明了如何计算成绩：

#### 程序 6

```c
/* Program to illustrate the use of multidimensionalarray */
#include <stdio.h>
```

#### 程序 6

```c
/* Number of rows and columns in array */
#define ROLLNO 3
#define SUBJECT 4

/* Beginning of main function */
main()
{
    /* Declare variables */
    float f_mark[ROLLNO][SUBJECT], f_total[ROLLNO] = {0};
    int i_rctr, i_cctr;

    /* Read Marks and Calculate Total */
    for (i_rctr = 0; i_rctr < ROLLNO; i_rctr++)
    {
        for (i_cctr = 0; i_cctr < SUBJECT; i_cctr++)
        {
            printf(" Enter marks of subject %d for roll no. %d: ",
                   i_cctr + 1, i_rctr + 1);
            scanf("%f", &f_mark[i_rctr][i_cctr]);

            /* Calculate the total marks of each ROLLNO */
            f_total[i_rctr] = f_total[i_rctr] + f_mark[i_rctr][i_cctr];
        }
        printf("\n");
    }

    printf("\nRESULT SHEET: \n\n");
    /* Print Total Marks */
    printf("\n\t SUBJECT 1\tSUBJECT 2\tSUBJECT 3\tSUBJECT 4\tTotal\n");
    for (i_rctr = 0; i_rctr < ROLLNO; i_rctr++)
    {
        printf("\nROLLNO %d! ", i_rctr + 1);
        for (i_cctr = 0; i_cctr < SUBJECT; i_cctr++)
        {
            printf("%0.2f\t\t", f_mark[i_rctr][i_cctr]);
        }
        printf("%0.2f\t", f_total[i_rctr]);
        printf("\n");
    }

    return;
} /* End of function main */
```

##### 输出：

科目 1 学号 1 的成绩: 75

科目 2 学号 1 的成绩: 90

科目 3 学号 1 的成绩: 40

科目 4 学号 1 的成绩: 40

科目 1 学号 2 的成绩: 50

科目 2 学号 2 的成绩: 60

科目 3 学号 2 的成绩: 70

科目 4 学号 2 的成绩: 85

科目 1 学号 3 的成绩: 80

科目 2 学号 3 的成绩: 85

科目 3 学号 3 的成绩: 55

科目 4 学号 3 的成绩: 60

成绩单:

| 科目 1 | 科目 2 | 科目 3 | 科目 4 | 总分 |
| :--- | :--- | :--- | :--- | :--- |
