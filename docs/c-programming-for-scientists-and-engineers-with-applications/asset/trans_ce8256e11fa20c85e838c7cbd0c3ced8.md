

## 232 控制结构

```c
else {
    printf("z largest");
} else {
    if(y > z) {
        printf("y largest");
    } else {
        printf("z largest");
    }
}
```

这也可以用最少数量的大括号写如下：

```c
if(x > y)
    if(x > z)
        printf("x largest");
    else
        printf("z largest");
else
    if(y > z)
        printf("y largest");
    else
        printf("z largest");
```

`if` 或 `else` 之后的语句块可以是单个语句、一个重复结构，或者是由大括号括起来的一个或多个语句组成的序列。本质上，单个选择结构或重复结构可以被当作一个语句使用。

嵌套选择结构的特殊情况：当一个分支上没有语句时（如嵌套选择结构图 4.15 所示），代码必须指示这一点。这可以通过三种方法之一实现。

## 4.4 控制结构的堆叠与嵌套 233

![](img/8356e6c3bfe3b10354682c60b1e74b1d_252_0.png)

图 4.15 嵌套选择结构

通过使用所示的大括号：

```c
if(value found)
{
  if(value > 0)
  {
    s = sqrt(value);
    printf("%f %f", value ,s);
  }
} else
  printf("no value found");
```

或者通过使用所示的空-else 语句：

```c
if(value found)
  if(value > 0)
  {
    s = sqrt(value);
    printf("%f %f", value, s);
  }
  else;
```

```c
else
printf("no value found");
```

或者通过使用空块：

```c
if(value found)
  if(value > 0)
{
    s = sqrt(value);
    printf("%f %f"
}
else
printf("no value found");
```

在第一个版本中，嵌入的选择结构是一个 `if...else` 而不是 `if...else...`，需要额外的一组括号以便计算机知道 `else` 属于哪一个。在第二和第三版本中，通过让两个选择结构都采用 `...else...` 形式避免了这个问题，尽管内部的 `else` 没有代码体。注意，在第一个 `else` 之后分号或空大括号表示空分支。

while 循环内部嵌套选择结构：假设候选人 A 和 B 正在竞选。随着选区结果出来，每个候选人的票数被总计，总票数相加。假设有 100 个选区。
图 4.16 流程的代码如下：

```c
int totvote = 0, atot = 0, btot = 0, b;
int num_precincts = 1; /*选区计数器*/
while(num_precincts <= 100) { /*选区总数*/
{
    printf("Enter the number of votes for a and b");
    printf("for precinct %d", num_precincts);
    sscanf("%d %d", &a, &b);
    totvote = totvote + a + b;
    atot = atot + a;
    btot = btot + b;
    if(atot > btot)
```

![](img/8356e6c3bfe3b10354682c60b1e74b1d_254_0.png)

图 4.16 嵌套在 while 循环中的选择结构

```c
    printf("\na ahead with %d precincts reporting\n",num_precincts);
    else
    printf("\nb ahead with %d precincts reporting\n",num_precincts);
    num_precincts = num_precincts + 1;
}
printf("\na: %d votes b: %d final count\n", atot, btot);
```

## 236 控制结构

![](img/8356e6c3bfe3b10354682c60b1e74b1d_255_0.png)

图 17 嵌套在选择结构中的 while 循环

所示图 17 流程图的 C 代码如下：

```c
fscanf(inptr, "%f", &date_measured);
if(date_measured > 0)
{
    int count = 0;
    float total = 0;
    while(fscanf(inptr, "%f", &measurement) != EOF)
    {
        total = total + measurement;
        count = count + 1;
    }
    printf("average of measurements is: %f", total/count);
}
else
    printf("not correct data");
```

注意 `inptr` 是包含测量文件的指针。

## 4.4.3 复习题

1. 判断下列语句对错：
    a. 控制结构的嵌套取决于逻辑。
    b. 选择结构可以嵌套在 while 结构内部。
    c. while 循环可以嵌套在选择结构内部。
    d. 结构可以嵌套三层。
2. 绘制一个流程图，判断三个值是否构成三角形。判断三角形是等边三角形、等腰三角形还是斜三角形。

## 4.5 习题与程序

这些题目源自工程与科学。示例程序展示了各种控制结构的使用。在某些解决方案中输入数据是交互式的。

## 4.5.1 电路的阻抗与电感

题目：编写一个程序计算电路的阻抗 Z 和电感 L，给定电压 V、电流 I (安培)、电阻 R (欧姆) 和频率 (赫兹)，共六个电路。

此示例演示了由计数器控制的重复。电路位于所示 AC 电路![](img/8356e6c3bfe3b10354682c60b1e74b1d_257_0.png)

数据：电压 (伏特)、电流 (安培)、电阻 (欧姆) 和频率 (赫兹)。

方法：
$Z = V/I$
$Z^2 = R^2 + X_L^2$
$X_L = \sqrt{Z^2 - R^2}$
$L = X_L / (2\pi)$
其中 $L$ 是电感，$X_L$ 是电抗，$Z$ 是阻抗。

伪代码：
对于每组六个值
输入电压、电流和频率
计算阻抗 $Z = V/I$
计算电抗 $X_L = \sqrt{Z^2 - R^2}$
计算电感 $L = X_L / (2.0 \times f)$
输出电压、电感、电抗
停止

```c
程序
/******************************************************
/* 电阻和电抗中的电感 */
/* 六组值的 AC 电路 */
/******************************************************
/* 常数： */
/* PI = 3.141593 */
/* 输入变量： */
/* voltage (伏特) */
/* current (安培) */
/* resistance (欧姆) */
/* frequency (赫兹) */
/* 计算变量： */
/* impdnc - 阻抗 */
/* indctn - 电感 */
/* rectnc - 电抗 */
```

```c
#include <stdio.h>
#include <math.h>
int main() 
{
    int i;
    float voltage, current, frequency;
    float impdnc, indctn, rectnc;
    const float PI = 3.141593;

    /* 输入六组值 */

    printf("INPUT              OUTPUT\n");
    for(i = 0; i < 6; i++) {
        scanf("%f %f %f", &voltage, &current, &frequency);

        impdnc = voltage / current;
        rectnc = sqrt(impdnc * impdnc - resistance);
        indctn = rectnc / (2.0 * PI * frequency);

        printf("%5.2f %5.2f %5.2f %5.2f\n", voltage, current, rectnc, indctn);
    }

    return 0;
}
```

| INPUT | OUTPUT |
| :--- | :--- |
| 120. 8. 50. | 120.00 6.00 0.02 |
| 250. 14. 7. 50. | 250.00 14.00 16.43 0.05 |
| 150. 16. 9. 50. | 150.00 16.00 2.62 0.01 |
| 100. 10. 5. 50. | 100.00 10.00 8.66 0.03 |
| 220. 12. 50. | 220.00 12.00 16.50 0.05 |
| 300. 19. 9. 50. | 300.00 19.00 12.97 0.04 |

## 5.2 射体的高度

题目：编写一个程序，在忽略空气阻力的情况下，计算射体运行的最大高度，给定不同的初始速度。此示例演示了由终止限制控制的重复。

方法：物体的质量为 $m$，初始速度为 $v_0$ (每秒)，最后的初始速度为 $v_f$ (英秒)。

根据运动方程：
$w = mg, \sum F_z = maz$.

将这些方程应用于射体得到：
$-mg = ma_c$ 得 $a_c = -g$

## 控制结构

根据运动学：$v^2 = v_0^2 + 2a_t(s_f - s_0)$
$0 = v^2 + 2a_t(h - 0)$
$2a_th = -v^2$
$h = \frac{-v^2}{2a_t}$

# 伪代码

对于每个初始速度
高度 $\leftarrow$ (初始速度 * 初始速度) / (2.0 * 加速度)
输出初始速度和高度

结束循环
停止

```c
程序
/******************************************************
/* 射体在电阻中的电感确定 */
/******************************************************
/* 常数： */
/* GRAV_ACCEL = 32.2 ft/sec² 重力 */
/* 输入变量： */
/* inititvel - 发射的初始速度 ft/sec² */
/* 计算变量： */
/* height - 高度 */
```

