

## 3. 手动示例

假设数据文件包含以下五组数据：

| 识别 | 峰值风速 |
|---|---|
| 142 | 38 |
| 153 | 135 |
| 162 | 59 |
| 177 | 76 |
| 181 | 63 |

我们的程序应生成以下报告：

### 有资格成为飓风的风暴

| 识别 | 峰值风速 (mph) | 类别 |
|---|---|---|
| 153* | 135 | 4 |
| 177 | 76 | 1 |

请记住，星号标识风速最大的风暴。

## 4. 算法开发

我们首先开发分解大纲，因为它将解决方案分为一系列顺序步骤。要打印飓风风暴的信息，我们不需要数组。我们在读取文件时可以确定这些信息，因为飓风状态仅取决于风速。但是，由于我们需要使用星号来指示峰值风速的风暴，我们需要将所有信息存储在数组中。在确定最大风速后，我们可以再次遍历数据，并在正确的行上打印带有星号的飓风信息。

### 分解大纲

- 1. 将风暴数据读入数组，并确定最大风速。
- 2. 计算强度类别并打印飓风风暴的信息；在最大值处放置星号。

我们将确定强度类别的步骤放入一个函数中：

### 伪代码细化

```
main: if file cannot be opened
        print error message
else
    read data into arrays, and determine max speed, npts
    set k to 0
    while k < npts-1
        if mph[k] > 74
            if mph[k] = max speed
                print id[k], *, mph[k], category(mph[k])
            else
                print id[k], mph[k], category(mph[k])
    add 1 to k
```

```
category(mph):
    category = 1;
    if mph >= 96
        category = 2
    if mph >= 111
        category = 3
    if mph >= 131
        category = 4
    if mph >= 155
        category = 5
```

伪代码中的步骤现在足够详细，可以转换为 C 语言：

```c
/*-------------------------------------------------------------*/
/*
 * Program chapter5_3
 *
 * This program reads storm values from a data file
 * and prints a hurricane report.
 */
#include <stdio.h>
#define N 500
#define FILENAME "storms1.txt"

int main(void)
{
    /* Declare and initialize variables. */
    int k=0, npts, id[N];
    double mph[N], max=0;
    FILE *storms;
    int category(double speed);

    /* Open file, read data into an array,
     * and determine maximum wind speed. */
    storms = fopen(FILENAME,"r");
    if (storms == NULL)
        printf("Error opening input file.\n");
    else
    {
        /* Read data and determine maximum mph. */
        while ((fscanf(storms,"%d %lf",&id[k],&mph[k])) == 2)
        {
            if (mph[k] > max)
                max = mph[k];
            k++;
        }
        npts = k;

        /* Print hurricane report. */
        if (max >= 74)
        {
            printf("Storms that Qualify as Hurricanes \n");
            printf("Identification Peak Wind (mph) Category \n");
        }
        else
            printf("No hurricanes in the file \n");
        for (k=0; k<npts-1; k++)
            if (mph[k] >= 74)
                if (mph[k] == max)
                    printf("%d* %d %d \n", id[k], mph[k], category(mph[k]));
                else
                    printf("%d %d %d \n", id[k], mph[k], category(mph[k]));

        /* Close file. */
        fclose(storms);
    }

    /* Exit program. */
    return 0;
}
/*------------------------------------------------------------*/
/* This function determines the hurricane intensity
/* category. */
int category(double speed)
{
/* Declare variables. */
int intensity=1;
/* Determine category. */
if (speed >= 96)
    intensity = 2;
if (speed >= 111)
    intensity = 3;
if (speed >= 131)
    intensity = 4;
if (speed >= 155)
    intensity = 5;
/* Return intensity. */
return intensity;
}
/*------------------------------------------------------------*/
```

## 5. 测试

我们将使用包含手动示例的文件测试我们的程序。这将产生以下交互：

```
Storms that Qualify as Hurricanes
Identification   Peak Wind (mph)   Category
153*             135               4
177              76                1
```

## 修改！

这些问题与前面的打印飓风强度报告的程序有关。

- 1. 修改程序，使其仅打印风速最大的飓风的信息。
- 2. 修改程序，使其还打印数据文件中的风暴数量。
- 3. 修改程序，使其还打印数据文件中的飓风数量。
- 4. 修改程序，使其打印每个类别中的飓风数量。

## 5.3 应用问题求解：分子量

化学反应在许多科学和工程系统中发挥着重要作用。理解和控制化学反应使石油工程师能够提高处理石油和天然气资源所需炼油厂的效率。了解在强磁场影响下处于极高温度的完全电离气体的行为和反应，将是发展受控核聚变的重要一步。在基因工程中，鉴定 DNA 中的氨基酸是开发合成新产品技术的关键步骤。

从化学式计算分子量是任何涉及化学反应的应用中的常见任务。编写一个程序，从键盘读取化学式，然后计算相应的分子量。我们假设该程序将用于处理蛋白质中氨基酸的基因工程实验室。氨基酸仅含有氧 (O)、碳 (C)、氮 (N)、硫 (S) 和氢 (H) 原子。例如，丙氨酸的化学式为 O2C3NH7；因此，丙氨酸含有两个氧原子、三个碳原子、一个氮原子和七个氢原子。(表 5.3 包含氨基酸中的原子。) 程序的输入是一组指定化学式的字符。有效字符是 O、C、N、S 和 H 的缩写，我们将允许这些字符为大写或小写。每个元素后面还可以跟一位或两位数字，用于指定元素的原子数量。因此，丙氨酸的输入字符可以是 O2C3NH7 或 o2c3nh7。如果元素不是五个指定元素之一，或者公式以数字开头，则会发生错误。使用以下分子量：

| 氧 | 15.9994 | 硫 | 32.066 |
| 碳 | 12.011 | 氢 | 1.00794 |
| 氮 | 14.00674 | | |

### 表 5.3 氨基酸分子

| 氨基酸 | O | C | N | S | H |
|---|---|---|---|---|---|
| 丙氨酸 | 2 | 3 | 1 | 0 | 7 |
| 精氨酸 | 2 | 6 | 4 | 0 | 15 |
| 天冬酰胺 | 3 | 4 | 2 | 0 | 8 |
| 天冬氨酸 | 4 | 4 | 1 | 0 | 6 |
| 半胱氨酸 | 2 | 3 | 1 | 1 | 7 |
| 谷氨酸 | 4 | 5 | 1 | 0 | 8 |
| 谷氨酰胺 | 3 | 5 | 2 | 0 | 10 |
| 甘氨酸 | 2 | 2 | 1 | 0 | 5 |
| 组氨酸 | 2 | 6 | 3 | 0 | 10 |
| 异亮氨酸 | 2 | 6 | 1 | 0 | 13 |
| 亮氨酸 | 2 | 6 | 1 | 0 | 13 |
| 赖氨酸 | 2 | 6 | 2 | 0 | 15 |
| 甲硫氨酸 | 2 | 5 | 1 | 1 | 11 |
| 苯丙氨酸 | 2 | 9 | 0 | 1 | 11 |
| 脯氨酸 | 2 | 5 | 1 | 0 | 10 |
| 丝氨酸 | 3 | 3 | 1 | 0 | 7 |
| 苏氨酸 | 3 | 4 | 1 | 0 | 9 |
| 色氨酸 | 2 | 11 | 2 | 0 | 11 |
| 酪氨酸 | 3 | 9 | 1 | 0 | 11 |
| 缬氨酸 | 2 | 5 | 1 | 0 | 11 |

### 1. 问题描述

计算氨基酸化学式的分子量。

### 2. 输入/输出描述

程序的输入是从键盘输入的化学式，输出是在计算机屏幕上显示的相应分子量。

![](img/02c4582f051c5b51776411c92b079035_249_0.png)

### 3. 手动示例

如果输入是丙氨酸的化学式 O2C3NH7，则相应输出应按以下方式计算：

两个氧原子：
2 · 15.9994 = 31.9988

三个碳原子：
3 · 12.011 = 36.033

一个氮原子：
1 · 14.00674 = 14.00674

七个氢原子：
7 · 1.00794 = 7.05558

总分子量为 89.09412。

### 4. 算法开发

我们首先开发分解大纲，因为它将解决方案分解为一系列顺序步骤：

### 分解大纲

- 1. 读取化学式。
- 2. 计算分子量。
- 3. 打印分子量。

步骤 1 涉及从键盘读取字符并将其存储在整数数组中。步骤 2 涉及检查字符（也称为解析），首先确定每个元素，然后确定每个元素的原子数量。由于此比较需要多个步骤，我们将在一个函数中实现此计算。在主函数中，我们将单个原子量乘以相应的原子数量；然后将值加到总计中。请注意，我们需要将原子数量从字符数字转换为数值，以便进行乘法运算。由于数字在排序序列中是连续的，数字的数值等价物可以通过从中减去值 ‘0’ 来获得。

步骤 3 涉及打印最终分子量。在此步骤中，如果输入字符无法正确分析，我们还将打印错误消息。现在可以为主函数和 atomic_wt 函数开发伪代码细化：

### 伪代码细化

```
main: print message to the user
      set k to 0
      while more characters
          read formula[k]
          increment k by 1
      set k to 0
      while more characters
          convert current character to uppercase
          determine atomic weight
          determine if digits follow
          compute weight and add to total
      print molecular weight
```

解析

