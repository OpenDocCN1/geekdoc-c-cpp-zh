
```c
reynoldsnum[i] = (density * velocity * length) / viscosity;
}
printf("\nIndex | Velocity | Reynolds Number\n");
for (i = 0; i < ARSIZE; i++) {
    printf("%d | %d | %.2f\n", i+1, 100 + (i * 100), reynoldsnum[i]);
}
return 0;
}
```

#### 输入与输出
| Index | Velocity | Reynolds Number |
|---|---|---|
| 1 | 100 | 15328.95 |
| 2 | 200 | 30657.90 |
| 3 | 300 | 45986.84 |
| 4 | 400 | 61315.79 |
| 5 | 500 | 76644.74 |
| 6 | 600 | 91973.69 |
| 7 | 700 | 107302.64 |
| 8 | 800 | 122631.59 |
| 9 | 900 | 137960.53 |
| 10 | 1000 | 153289.48 |

### 7.6.2 应力与应变

计算钢承受 10,000 到 100,000 磅（增量为 10,000 磅）压缩载荷时的应力和应变。柱的直径以英寸输入。钢的弹性模量为 $E = 30 \times 10^6$ psi。将载荷、应力和应变存储在并行数组中。以表格形式输出载荷、应力和应变。此示例展示了并行数组的构建。应应变的公式如下：

应力由公式给出：$\sigma = p(\pi d^2/4)$
应变由公式给出：$\epsilon = \sigma/E$

其中 $\sigma$ 是单位为 pounds/in² 的应力，
- $\epsilon$ 是无量纲应变，
- $p$ 是单位为磅的载荷，
- $d$ 是单位为英寸的直径，以及
- $E$ 是单位为 pounds/in² 的弹性模量。

#### 程序
> /*****************************************************/
> /************************************/
> /* 计算钢柱的应力和应变                 */
> /************************************/
> /* 常量: */
> /* E = 30e6 */
> /* PI = 3.141593 */
> /* 输入变量: */
> /* diameter = 单位为英寸的柱直径 */
```c
#include <stdio.h>
#define ARSIZE 10
int main() {
    int i;
    const float E = 30e6;
    const float PI = 3.141593;
    float diameter;
    float load[ARSIZE];
    float stress[ARSIZE];
    float strain[ARSIZE];
    printf("Input the diameter of cylinder in inches: ");
    scanf("%f", &diameter);
    for (i = 0; i < ARSIZE; i++) {
        load[i] = 10000 + (i * 10000);
        stress[i] = load[i] / (PI * (diameter * diameter) / 4.0);
        strain[i] = stress[i] / E;
    }
    printf("\nIndex | Load | Stress | Strain\n");
    for (i = 0; i < ARSIZE; i++) {
        printf("%d | %d | %.2f | %.6f\n", i+1, load[i], stress[i], strain[i]);
    }
    return 0;
}
```

#### 输入与输出
| Index | Load | Stress | Strain |
|---|---|---|---|
| 1 | 10000 | 15328.95 | 0.000511 |
| 2 | 20000 | 30657.90 | 0.001022 |
| 3 | 30000 | 45986.84 | 0.001533 |
| 4 | 40000 | 61315.79 | 0.002044 |
| 5 | 50000 | 76644.74 | 0.002555 |
| 6 | 60000 | 91973.69 | 0.003066 |
| 7 | 70000 | 107302.64 | 0.003577 |
| 8 | 80000 | 122631.59 | 0.004088 |
| 9 | 90000 | 137960.53 | 0.004599 |
| 10 | 100000 | 153289.48 | 0.005110 |

```c
/*
/* 输出变量:
/*
/* stress - 压缩应力，单位 lbs/in2
/*
/* strain - 压缩应变，无量纲
/*
/* 调用的函数:
/*
/*     -无
/*\n/*
/*
/*
/* ******************************************************************/
```
```c
#include <stdio.h>
#define SIZE 10
int main ()
{
    int i;
    const float PI = 3.141593;
    const float E = 30E06;
    float diameter, area, load, stress[SIZE], strain[SIZE];
    printf("Enter the diameter (inches): ");
    scanf("%f", &diameter);
    area = PI * (diameter * diameter) / 4.0;
    load = 10000.00;
    for(i = 0; i < SIZE; i++)
    {
        stress[i] = load / area;
        strain[i] = stress[i] / E;
        load += 10000.00;
    }
    printf("\ncol diameter: %6f\n", diameter);
    printf(" index compload stress strain\n");
    load = 10000.00;
    for(i = 0; i < SIZE; i++)
    {
        printf("%4d. \t%10.2f \t%9.2f \t%12.8f\n",
               i, load, stress[i], strain[i]);
        load += 10000.00;
    }
    return 0;
}
```

# 输出

输入直径（英寸）： 4

| 列 | 组合载荷 | 应力 | 应变 |
|---|---|---|---|
| 0. | 10000.00 | 795.77 | 0.00002653 |
| 1. | 20000.00 | 1591.55 | 0.00005305 |
| 2. | 30000.00 | 2387.32 | 0.00007958 |
| 3. | 40000.00 | 3183.10 | 0.00010610 |
| 4. | 50000.00 | 3978.87 | 0.00013263 |
| 5. | 60000.00 | 4774.65 | 0.00015915 |
| 6. | 70000.00 | 5570.42 | 0.00018568 |
| 7. | 80000.00 | 6366.20 | 0.00021221 |
| 8. | 90000.00 | 7161.97 | 0.00023873 |
| 9. | 100000.00 | 7957.75 | 0.00026526 |

### 7.6.3 标准差

问题：给定某科学实验的测量值，计算记录的实验值的平均值和标准差。打印出平均值一个标准差之外的实验值。本示例展示了如何使用函数处理数组。

方法 计算数值的平方和

![](img/8356e6c3bfe3b10354682c60b1e74b1d_445_0.png)

计算数值之和的平方

![](img/8356e6c3bfe3b10354682c60b1e74b1d_445_1.png)

以及平均值

![](img/8356e6c3bfe3b10354682c60b1e74b1d_445_2.png)

标准差的公式如下：

标准差 = $\sqrt{\frac{\sum_{i=1}^{n} x_i^2 - \frac{1}{n}\left(\sum_{i=1}^{n} x_i\right)^2}{n-1}}$

# 数据

十个真实的测量数据值

# 伪代码

```
main:
将测量数据值输入数组
调用 funcmean
调用 funcstdev
打印平均值和标准差
打印标准差范围之外的数值
```
停止

# 函数 funcmean:

累加数据值

平均值 = 数据值和 / 数值个数

结束

# 函数 funcstdev:

计算数值的平方和以及数值之和

计算数值之和的平方

计算平均值

计算标准差

返回平均值和标准差

# 程序

```c
********************************************************************/
/* 主：标准差和极值 */
********************************************************************/
/* 输入变量:                                     */
* expdata[ARSIZE] - 实验数据 */
/* 输出变量:                                    */
* stdev - 标准差 */
* expdata - 极值 */
* mean - 平均值                                     
/* 调用的函数:                                     */
* funcmean - 计算平均值的函数 */
* funcstdev - 计算标准差的函数 */
****************************************************/
```
```c
#include <stdio.h>
#include <math.h>
#define ARSIZE 10
float funcmean(float [ ], int);
float funcstdev(float [ ], int);
int main()
{
    int i;
    float expdata[ARSIZE], mean, stdev;
    printf("Input ten data\n");
    for(i = 0; i < ARSIZE; i++)
        scanf("%f", &expdata[i]);
    mean = funcmean(expdata, ARSIZE);
    printf("mean = %5f\n", mean);
    stdev = funcstdev(expdata, ARSIZE);
    printf("standard deviation = %5f\n", stdev);
    printf("The extreme values:\n");
    for(i = 0; i < ARSIZE; i++)
```
```c
{
  if(fabs(expdata[i] - mean) > stdev)
    printf("%.2f\n", expdata[i]);
  }
  return 0;
}
```
```c
/****************************************************************
/* 函数: funcmean - 计算平均值 */
/****************************************************/
/* 输入参数:                                                   */
* expdata[n]- - 实验数据 */
* n - 数值个数                                           
/* 局部变量:                                                      */
* mean - 平均值                                                     
* sum - 数值之和                                            
/* 返回值:                                                        */
* mean - 平均值                                                     
/* 调用的函数: 无                                               */
/****************************************************/
```
```c
float funcmean(float expdata[ ], int n)
{
  int i;
  float sum = 0, mean;
  for(i = 0; i < n; i++)
    sum += expdata[i];
  mean = sum / n;
  return mean;
}
```
```c
/****************************************************/
/* 函数: funcstdev - 计算标准差 */
/****************************************************/
/* 输入参数:                                                   */
* expdata[n]- - 实验数据 */
* n - 数值个数                                           
/* 局部变量:                                                      */
* sumqr - 数值的平方和 */
* sqsum - 数值之和的平方                               */
/* 返回值:                                                        */
* stdev - 标准差                                           
/* 调用的函数: 无                                               */
/****************************************************/
```
```c
float funcstdev(float expdata[], int n)
{
    int i;
    float sum = 0, sumqr = 0, sqsum, stdev;
    for(i = 0; i < n; i++) {
        sum += expdata[i];
        sumqr += expdata[i] * expdata[i];
    }
    sqsum = sum * sum;
    stdev = sqrt((sumqr - (sqsum / n)) / (n - 1));
    return stdev;
}
```

# 输入和输出

输入十个值

12.0 5.0 2.0 19.0 7.0 11.0 6.0 8.0 10.0 9.0

mean = 8.90

standard deviation = 4.63

极值:

2.00

19.00

## 7.6 示例程序

### 7.6.4 最大值最小值

问题：编写一个程序，找到并打印存储在数组中的实数最大值和最小值。使用函数寻找最大最小值。本示例展示了使用函数名和地址的函数。由于函数返回两个值，最大最小值必须通过地址传递。

方法

+ 将值输入数组

假设第一个值是最大值最小值

遍历数组的每个值：

  如果该值小于最小值，更新最小值

  如果该值大于最大值，更新最大值

  结束循环

输出最大值最小值

停止

数据

+   整数列表。

伪代码

```
main:
输入包含 n 个元素的数组
调用 maxmin(n, a, amax, amin)
打印 amax 和 amin
停止
```

```
function maxmin:
amax ← a[0]
amin ← a[0]
for 每个数组元素 i
if a[i] > amax
amax ← a[i]
else if a[i] < amin
amin ← a[i]
end for
return
end
```

# 432 一维数组
