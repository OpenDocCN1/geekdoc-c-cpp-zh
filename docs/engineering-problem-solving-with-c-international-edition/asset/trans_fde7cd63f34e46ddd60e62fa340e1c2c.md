

/* Read and print information from the file. */
storms = fopen(FILENAME,"r");
if (storms == NULL)
    printf("Error opening data file. \n");
else
{
    while (fscanf(storms,"%s %d %d",h1.name,&h1.year,
        &h1.category) == 3)
    print_hurricane(h1);
}
fclose (storms);
/* Exit program. */
return 0;
}

/*-----------------------------------------------------*/
/* This function prints the hurricane information.     */
/*-----------------------------------------------------*/
void print_hurricane(struct hurricane h)
{
    printf("Hurricane: %s \n",h.name);
    printf("Year: %d, Category: %d \n",h.year,h.category);
    return;
}
/*-----------------------------------------------------*/

当编写用于修改结构体中数据成员值的函数时，必须使用指向结构体的指针作为函数参数。这样可以让函数直接访问结构体的数据成员。当通过指向结构体的指针访问数据成员时，使用指针运算符（->）而不是结构体成员运算符。此技术在第 7.6 节中演示，我们将在其中介绍动态数据结构。

## 返回结构体的函数

函数可以定义为返回结构体类型的值。函数被调用后，整个结构体将返回给调用函数。为举例说明，我们介绍一个与海啸相关的新结构体。假设我们正在处理与海啸相关的信息。该信息包括海啸的日期（月、日、年）、最大高度（英尺）、死亡人数和地点。月、日、年和死亡人数由整数表示，浮点数表示最大高度，地点由字符串表示。因此，表示该信息的结构体可以定义如下：

```
struct tsunami
{
    int mo, da, yr, fatalities;
    double max_height;
    char location[20];
};
```

我们现在介绍一个从键盘读取信息、将其保存在结构体中，然后将信息返回给主函数的函数。假设前面的结构体在主函数中定义，并且函数原型通过以下语句定义：

```
struct tsunami get_info(void);
```

我们将使用一个与用户交互以获取信息，然后以结构体形式返回该信息的函数。代码如下：

```
/*----------------------------------------------------------*/
/* This function gets information from the user to enter    */
/* into a tsunami structure.                                */
/*----------------------------------------------------------*/
struct tsunami get_info(void)
{
    /* Declare variables.    */
    struct tsunami t1;

    printf("Enter information for tsunami in following order: \n\n");
    printf("Enter month, day, year, number of deaths: \n");
    scanf("%d %d %d",&t1.mo,&t1.da,&t1.yr,&t1.fatalities);
    printf("Enter location (<20 characters, no spaces): \n");
    scanf("%s",t1.location);
    return(t1);
}
/*----------------------------------------------------------*/

- 修改！
- 1. 编写一个函数，读取结构体类型 hurricane 变量的用户信息。
- 2. 编写一个函数，打印结构体类型 tsunami 变量的海啸信息。

## 7.3 应用问题求解：指纹分析

在本节中，我们将使用本章介绍的新语句来解决与指纹分析相关的问题。指纹可分为三类：环纹、涡纹和弓纹。大约 60% 至 65% 的所有指纹是环纹；大约 30% 至 35% 是涡纹，大约 5% 是弓纹。为了减少数据库中需要与未知指纹匹配的指纹数量，我们可以消除与不同类别手指的匹配。例如，不需要将涡纹指纹与弓纹指纹进行匹配。事实上，已经开发出一些技术，可以查看所有 10 个手指的类别，并立即从比较中排除数据库的大部分。这些技术大致基于亨利技术，这是进行指纹识别的早期方法之一。

假设我们将要实现的技术会为带有 10 个手指的指纹记录分配一个数字。我们将根据每个指尖是否为涡纹来为其分配一个数字。指尖将标识为 R（代表右手）或 L（代表左手）。此外，第二个字母将手指标识为 t（拇指）、i（食指）、m（中指）、r（无名指）和 p（小指）。每个指尖的值分配如下：

- 如果 Rt 或 Ri 是涡纹，其值为 16。
- 如果 Rm 或 Ri 是涡纹，其值为 8。
- 如果 Rp 或 Lt 是涡纹，其值为 4。
- 如果 Li 或 Lm 是涡纹，其值为 2。

所有其他值均为零。

我们现在计算以下分数：

```
overall category = (Ri + Rr + Lt + Lm + Lp + 1)/
(Rt + Rm + Rp + Li + Lr + 1)
```

请注意，此类别不能为 0，且分母不能为 0。计算出此类别后，将其与指纹一起存储在记录中。一旦计算出未知指纹的类别，数据库中就有一小部分类别可能匹配。因此，查找匹配项只需比较几千个指纹，而无需比较数百万个指纹。此搜索将比较未知指纹的细节特征点与总体类别值接近未知指纹总体类别值的指纹的细节特征点。

在本节中，我们将开发一个 C 函数，该函数接收存储在结构体中的指纹信息集。我们将计算指纹的总体类别并将其存储在结构体中。因此，此函数可用于为未知指纹分配总体类别编号，也可用于循环中计算数据库中指纹的总体类别编号。

![](img/02c4582f051c5b51776411c92b079035_365_0.png)

### 1. 问题描述

编写一个函数，用于计算指纹的总体类别编号。

### 2. 输入/输出描述

以下图显示，程序的输入是 10 个指纹的类别。输出是根据此信息计算出的总体类别。

![](img/02c4582f051c5b51776411c92b079035_365_1.png)

### 3. 手算示例

假设十指指纹中的涡纹出现在右拇指、右无名指和左中指。各个手指的值均为 0，以下情况除外：

- Rt = 16
- Rr = 8
- Lm = 2

如果我们随后计算总体类别，则得到：

overall category = (8 + 2 + 1)/(16 + 1) = 11/17 = 0.65

### 4. 算法开发

我们首先开发分解大纲，因为它将解决方案划分为一组顺序步骤。

### 函数的分解大纲

1. 从函数输入获取指纹数据。
2. 根据指纹信息计算总体类别。
3. 将总体类别存储在指纹结构体中。

我们还需要开发一个可用于测试此函数的程序。测试程序的分解大纲如下：

### 测试程序的分解大纲

1. 从用户处读取指纹信息。
2. 使用函数计算总体类别。
3. 打印总体类别。

这些算法很简单，因此我们可以直接从分解大纲转到 C 代码。

```
/*----------------------------------------------------------*/
/* Program chapter7_4                                     */
/*                                                        */
/* This program stores fingerprint information in a structure. */
/* It then references a function to compute the overall category.*/

#include <stdio.h>

/* Define a structure for the fingerprint information.    */
/* The order for fingertips is right hand, thumb to pinky,  */
/* and left hand, thumb to pinky. The codes are L for loops, */
/* W for whorls, and A for arches.                          */
struct fingerprint
{
    int ID_number;
    double overall_category;
    char fingertip[10];
};

int main(void)
{
    /* Declare and initialize variables.                   */
    struct fingerprint new_print;
    double compute_category(struct fingerprint f);

