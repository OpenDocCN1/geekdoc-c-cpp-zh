

### 程序

```c
#include<stdio.h>
#include<math.h>
int fac(int x)
{
        int i, fac = 1;
        for (i = 1; i <= x; i++)
                fac = fac * i;
        return fac;
}
int main()
{
        float x, Q, sum = 0;
        int i, j, limit;
        printf("Enter the value of x of sinx series:  ");
        scanf("%f", &x);
        printf("Enter the limit upto which you want to expand the series : ");
        scanf("%d", &limit);
        Q = x;
        x = x * (3.1415 / 180);
        for (i = 1, j = 1; i <= limit; i++, j = j + 2)
        {
                if (i % 2 != 0)
                {
                        sum = sum + pow(x, j) / fac(j);
                }
                else
                {
                        sum = sum - pow(x, j) / fac(j);
                }
        }
        printf(" sin(%0.1f) : %f", Q, sum);
        return 0;
}
```

### 输出

```
Enter the value of x of sinx series : 40
Enter the limit upto which you want to expand the series : 5
sin(40.0): 0.642772
```

![](img/35ea447eca4d04af54f37bf3d3ca337d_99_0.png)

## 17) 编写一个程序，判断给定整数是否为素数，并生成给定范围内的素数。

### 算法

- 步骤 1：开始
- 步骤 2：输入并读取数字为 Num
- 步骤 3：设置 counter = 0；
- 步骤 4：如果 Num <= 1
  - 输出“Number is not Prime Number”
- 步骤 5：如果 for i = 2
- 步骤 6：如果 counter = 0，则
  - 输出“Number is Prime Number”
  - 否则
  - 输出“Number is not Prime Number”
- 步骤 7：停止

### 程序

```c
#include<stdio.h>
void main()
{
    int no, i = 2, p = 0;
    printf("Enter any no to detect prime or Not: ");
    scanf("%d", &no);
    do
    {
        if(no % i == 0)
            p = 1;
        i++;
    }
    while (i < no);
    if(p == 0 || no == 2)
        printf("\n The Given number is prime : %d", no);
    else
        printf("\n The number is NOT prime : %d", no);
}
```

### 输出

```
Enter any no to detect prime or Not : 22
The number is NOT prime : 22
```

## 19) 编写一个 C 程序：判断给定数字是否为完全数。

### 算法

```
Step 1: Start
Step 2: Read N
Step 3: sum = 0
Step 4: for i = 1 to N do
          1) begin
          2) if (N % i == 0)
          3) sum = sum + i
          4) end for
Step 5: if sum == n go to step 6 else go to step 7
Step 6: Write 'Given number is perfect number' go to step 8
Step 7: Write 'Given number is not a perfect number'
Step 8: Stop
```

### 程序

```c
#include<stdio.h>
#include<conio.h>
void main()
    /* main declaration */
{
    /* variable declaration */
    int i, sum = 0, N;
    clrscr();
    printf("Enter the values of n: ");
    scanf("%d", &N);
    for(i = 1; i < N; i++)
        {
            if(N % i == 0)
                {
                    sum = sum + i;
                }
        }
    if(sum == N)
        printf("The given number is perfect number");
    else
        printf("The given number is not a perfect number");
    getch();
}
```

### 输出

```
Enter the values of n : 28
The given number is perfect number.
```

![](img/35ea447eca4d04af54f37bf3d3ca337d_104_0.png)

## 练习题

### 编写一个“C”程序

- 1. 求圆的面积
- 2. 求三角形/矩形的面积
- 3. 求圆的周长
- 4. 求三角形/矩形的周长
- 5. 求单利
- 6. 求复利
- 7. 将摄氏温度转换为华氏温度
- 8. 计算 5 门科目的总分并求出百分比

![](img/35ea447eca4d04af54f37bf3d3ca337d_106_0.png)

## 数组和字符串

**结构：**

- 5.1 一维数组简介
  - 5.1.1 定义
  - 5.1.2 声明
  - 5.1.3 初始化
- 5.2 访问数组元素
- 5.3 从数组中查找最小值和最大值
- 5.4 反转数组
- 5.5 从数组中查找奇数、偶数和素数
- 5.6 二维数组
  - 5.6.1 定义
  - 5.6.2 声明数组变量
  - 5.6.3 二维数组的初始化
- 5.7 矩阵：加法、乘法、转置、对称性、上/下三角
  - 5.7.1 两个矩阵相加
  - 5.7.2 两个矩阵相乘
  - 5.7.3 输出矩阵的转置
  - 5.7.4 检查矩阵的对称性
  - 5.7.5 检查上三角
  - 5.7.6 检查下三角
- 5.8 字符串简介
  - 5.8.1 定义
  - 5.8.2 声明
  - 5.8.3 初始化
- 5.9 标准库函数
- 5.10 不使用标准库函数的实现

### 5.1 一维数组简介

数组是另一种变量或用户定义变量，在 C 语言中被广泛使用。数组是一个标识符，指向一组具有相同名称的数据项。因此，数组是相同类型数据项的集合，例如所有整数的集合、所有浮点数的集合、所有字符的集合。

各个数据项由其对应的数组元素（索引）表示。

假设 x 是一个包含 10 个元素的数组。第一个元素称为 x[0]，第二个称为 x[1]，依此类推。最后一个元素将是 x[9]。

![](img/35ea447eca4d04af54f37bf3d3ca337d_107_0.png)

数组中的每个成员（即每个单独的数据项）通过指定数组名后跟一个或多个下标（数组索引）来表示，每个下标括在方括号中。每个下标都必须表示为非负整数。在一个包含 n 个元素的数组中，数组元素为：

x[0]、x[1]、x[2]、...、x[n - 1]

如下图所示。数组的第一个元素使用记号 x[0] 表示，第二个元素使用记号 x[1] 表示，依此类推。

**声明**是提供变量的数据类型和标识符的语句。**标识符**是程序组件的名称。

#### 5.1.1 定义

只有一个下标的数组称为**一维数组**。

***示例：***

```c
int arr[10];
```

当你声明一个数组时，你声明的是一个包含多个相同类型数据项的数组；每个数据项是数组的一个**元素**。每个元素具有相同的数据类型，并且每个元素在内存中占据与其他元素相邻或连续的区域。数组中的所有元素都将存储在连续分配的内存中。

#### 5.1.2 声明

数组的声明方式与变量类似，唯一区别是每个数组名都必须指定大小。对于一维数组，通过在方括号中指定正整数表达式来完成，如下所示：

```c
data-type  array_name[expression]
```

其中 **data-type** 是数组元素的数据类型（int、float、char），**array_name** 是数组名，**expression** 是确定数组大小的正整数值常量。

#### 5.1.3 初始化

如果初始值数量多于声明的大小，编译器将产生错误。也就是说，语句

```c
int number[3] = {10, 20, 30, 40, 50};
```

将无法工作。这在 C 语言中是非法的。

#### 通过赋值初始化

```c
char arr_map[3];
arr_map[0] = 'S';
arr_map[1] = 'R';
arr_map[2] = 'D';
```

### 访问一维数组元素

数组从 0 开始索引，因此第一个数组元素位于索引 = 0，最高索引为 size_of_array - 1。要访问给定索引处的数组元素，应使用以下语法：

**示例代码**

```c
array_name[index_of_element];
```

要将数组的某个元素设置为某个值，应编写：

**示例代码**

```c
array_name[index_of_element] = value;
```

要访问 arr_map 的元素之一：

**示例代码**

```c
arr_map[0]; // value of 'S'
arr_map[1]; // value of 'R'
arr_map[2]; // value of 'D'
```

尝试访问索引 0 到 size_of_array - 1 范围之外的值会导致运行时错误。编译器不会报错，但程序在执行时会崩溃。

以下代码片段将数据放入容量为 40 个元素的整数类型数组项中

```c
for(i = 0; i < 40; i++)
{
    printf("Enter the item");
    scanf("%d", &items[i]);
}
```

上面的 for 循环要求用户输入 40 次数据项。开始时，i = 0，这使 scanf 语句初始化数组元素 items[0]（数组的第一个元素）。此过程持续到 i = 39，这将初始化数组的最后一个元素：items[39]。

注意，scanf 函数在 items[i] 前面包含一个与号（&），因为输入的是单个数组元素，而不是整个数组。

