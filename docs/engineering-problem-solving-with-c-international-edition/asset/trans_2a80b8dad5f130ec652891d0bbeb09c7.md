

## 3. 手算示例

对于手算示例，我们将计算纽约和伦敦之间的大圆距离。纽约的纬度和经度分别为北纬 40.75° 和西经 74°，伦敦的纬度和经度分别为北纬 51.5° 和西经 0°。

纽约的球面坐标为
φ = (90 − 40.75)° = 49.25(π/180) = 0.8596
θ = (360 − 74)° = 286(π/180) = 4.9916
ρ = 3960.

纽约的直角坐标（保留两位小数）为
x = ρ sin φ cos θ = 826.90
y = ρ sin φ sin θ = −2883.74
z = ρ cos θ = 2584.93.

同样，伦敦的直角坐标可计算为
x = 2465.16, y = 0, z = 3099.13.

两个向量之间夹角的余弦等于两个向量的点积除以它们长度的乘积，即 0.6408。使用反余弦函数，γ 可确定为 0.875 弧度。最后，纽约和伦敦之间的距离为
0.875 · 3960 = 3466 英里。

## 4. 算法开发

要开发算法，我们必须首先将问题的解分解为一组按顺序执行的步骤，如下所示：

### 分解大纲

- 1. 读取两个位置的纬度和经度。
- 2. 计算两个位置之间的距离。
- 3. 打印计算出的距离。

完成手算示例后，将分解转换为伪代码非常简单。由于其他程序也可能需要确定由纬度和经度指定的两点之间的距离，我们将使用函数来开发这些计算。

### 伪代码细化

```
main: read latitude and longitude for the two points
    compute great circle distance using a function, gc_distance
    print distance
gc_distance(lat1N,long1W,lat2N,long2W):
    convert latitude and longitude to spherical coordinates
    convert spherical coordinates to rectangular coordinates
    compute the angle between the two vectors
    compute the great circle distance for the arc between the two vectors
```

伪代码中的步骤现在足够详细，可以转换为 C 语言：

```c
/*-----------------------------------------*/
/* Program chapter4_4 */
/* */
/* This program determines the distance between two points */
/* that are specified with latitude and longitude values */
/* that are in the Northern Hemisphere. */
/*-----------------------------------------*/
#include <stdio.h>
#include <math.h>
#define PI 3.141593
int main(void)
{
 /* Declare variables and function prototype. */
 double lat1, long1, lat2, long2;
 double gc_distance(double lat1,double long1,
 double lat2,double long2);
 /* Get locations of two points. */
 printf("Enter latitude north and longitude west ");
 printf("for location 1: \n");
 scanf("%lf %lf",&lat1,&long1);
 printf("Enter latitude north and longitude west ");
 printf("for location 2: \n");
 scanf("%lf %lf",&lat2,&long2);
 /* Print great circle distance. */
 printf("Great Circle Distance: %f miles \n",
 gc_distance(lat1,long1,lat2,long2));
 /* Exit program. */
 return 0;
}
```

```c
/*-----------------------------------------*/
/* This function computes the distance between two */
/* points using great circle distances. */
/*-----------------------------------------*/
double gc_distance(double lat1,double long1,
double lat2,double long2)
{
 /* Declare variables. */
 double rho, phi, theta, gamma, dot, dist1, dist2,
 x1, y1, z1, x2, y2, z2;
 /* Convert latitude and longitude to rectangular coordinates. */
 rho = 3960;
 phi = (90 - lat1)*(PI/180.0);
 theta = (360 - long1)*(PI/180.0);
 x1 = rho*sin(phi)*cos(theta);
 y1 = rho*sin(phi)*sin(theta);
 z1 = rho*cos(phi);
 phi = (90 - lat2)*(PI/180.0);
 theta = (360 - long2)*(PI/180.0);
 x2 = rho*sin(phi)*cos(theta);
 y2 = rho*sin(phi)*sin(theta);
 z2 = rho*cos(phi);
/* Compute angle between vectors. */
 dot = x1*x2 + y1*y2 + z1*z2;
 dist1 = sqrt(x1*x1 + y1*y1 + z1*z1);
 dist2 = sqrt(x2*x2 + y2*y2 + z2*z2);
 gamma = acos(dot/(dist1*dist2));
 /* Compute and return great circle distance. */
 return gamma*rho;
}
/*--------------------------------------*/
```

## 5. 测试

我们从手算示例开始测试，它给出了以下交互：

```
Enter latitude north and longitude west for location 1:
40.75 74
Enter latitude north and longitude west for location 2:
51.5 0
Great Circle Distance: 3466 miles
```

## 修改！

这些问题与前面的程序有关，该程序计算北半球两点之间的大圆距离。

- 1. 编写一个函数，计算两个向量之间的夹角（以弧度为单位）。使用以下原型语句：
   double angle(double x1, double y1, double z1,
                double x2, double y2, double z2)
- 2. 修改本节开发的程序，使其使用问题 1 中的函数。
- 3. 修改程序，以允许用户输入北半球或南半球的纬度。程序应提示用户输入纬度值；然后提示用户输入 N 或 S 以指定半球。如果纬度在南半球，则将值的符号更改为负数以给出北纬参考。请注意，您不需要更改 gc_distance 函数——但您需要对南半球参考进行调整（以便计算从北半球参考开始）。
- 4. 修改程序，以允许用户输入西经或东经的经度。程序应提示用户输入经度值；然后提示用户输入 W 或 E 以指定半球。如果经度是东经参考，则用 360 减去该数字以给出西经参考。请注意，您不需要更改 gc_distance 函数——但您需要对东经参考进行调整（以便计算从西经参考开始）。
- 5. 修改程序，使其结合问题 3 和 4 的修改。因此，用户可以输入带有北纬或南纬参考的纬度，以及带有西经或东经参考的经度。同样，该函数不需要修改。

## 4.5 随机数

一组随机数不是由方程定义的；相反，它具有定义它的某些特征。这些特征包括最小值和最大值以及平均值。它们还指示可能的值是否等可能发生，或者某些值是否比其他值更可能发生。随机数序列可以通过实验生成，例如抛硬币、掷骰子或选择编号球。随机数序列也可以使用计算机生成。

许多工程问题在解决方案的开发中需要使用随机数。在某些情况下，这些数字用于开发复杂问题的模拟。模拟可以反复运行以分析结果；每次重复代表一次实验的重复。我们还使用随机数来近似噪声序列。例如，我们在收音机上听到的静电噪声是一个噪声序列。如果我们的测试程序使用代表无线电信号的输入数据文件，我们可能希望生成噪声并将其添加到语音信号或音乐信号中，以提供更真实的信号。

工程应用程序通常需要在指定值之间分布随机数。例如，我们可能希望生成 1 到 500 之间的随机整数，或者我们可能希望生成 5 和 -5 之间的随机浮点值。我们现在介绍在两个指定值之间生成随机数的讨论。生成的随机数是等可能发生的；也就是说，如果随机数应该是 1 到 5 之间的整数，那么集合 {1, 2, 3, 4, 5} 中的每个整数都是等可能发生的。另一种说法是，每个整数大约应该有 20% 的时间出现。任何值在指定集合中都是等可能出现的随机数也称为均匀随机数，或均匀分布随机数。

### 整数序列

标准 C 库包含一个名为 rand 的函数，它生成 0 到 RAND_MAX 之间的随机整数，其中 RAND_MAX 是在 stdlib.h 中定义的系统相关整数。（RAND_MAX 的常见值为 32,767。）rand 函数没有输入参数，并由表达式 rand() 引用。因此，要生成并打印两个随机数的序列，我们可以使用此语句：

```
printf("random numbers: %i %i \n", rand(), rand());
```

每次执行包含此语句的程序时，都会打印相同的两个值，因为 rand 函数生成指定序列中的整数。（由于此序列最终开始重复，它有时被称为伪随机序列，而不是

