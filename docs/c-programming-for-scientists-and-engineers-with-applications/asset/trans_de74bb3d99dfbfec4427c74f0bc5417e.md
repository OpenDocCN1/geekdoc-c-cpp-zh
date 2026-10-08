

```c
/* height - 射物体到达的高度 */
/* 输出变量: */
/* initvel - 射出的初始速度，单位 ft/sec* */
/* height - 射物体到达的高度 */
/****************************************************************```

```c
#include <stdio.h>

int main() {
    const float GRAV_ACCEL = 32.2;
    float initvel,height;

    printf("Initial Velocity \tHeight\n\n");
    initvel = 50;
    while(initvel <= 200) {
        height = - (initvel * initvel) / (2.0 * GRAV_ACCEL);
        printf("%6.2f\t%8.2f\n", initvel, -1.0 * height);
        initvel += 50;
    }
    return 0;
}
```

输出

Initial Velocity \tHeight
50.00	38.82
100.00	155.28
150.00	349.38
200.00	621.12
```

## 4.5.3 金属构件的剪切应力

问题：编写一个程序，计算并打印表格，显示具有不同偏移量的各种扭负载的圆棒的扭剪切应力。此示例演示了嵌套循环的使用。

数据

- 直径：5 和 6 英寸
- 负载：1000 和 12,000 磅
- 偏移：10, 15 和 20

![](img/8356e6c3bfe3b10354682c60b1e74b1d_263_0.png)

方法

设 D = 棒的直径
P = 扭负载（单位：磅）
L = 偏移量

扭剪切应力由公式给出

```
$T_s = \frac{16PL}{\pi D^3}$
```

伪代码

```
对于每个棒的直径
    输出棒的直径
    对于每个负载
        输出负载
        对于每个偏移
            剪切应力 ← (16 × 扭负载 × 长度偏移) / (π × 直径 × 直径)
            输出剪切应力
    结束循环
    结束循环
结束循环
停止
```

# 程序

```c
****************************************************************/
/* */
/* 打印扭剪切应力表 */
/* */
****************************************************************/
/* */ 常量: */
/* */
/* PI = 3.141593 */
/* */
/* 输入变量: */
/* */
/* diameter - 棒的直径 */
/* */ torsion_load - 扭负载 */
/* */ 施加的（磅） */
/* */ length_offset - 负载偏移长度（英寸） */
/* */
/* */ 计算变量: */
/* */
/* */
/* shear_stress - 剪切应力 */
/* */ 磅/平方英寸 */
/* */
/* */ 输出变量: */
/* */
/* */
/* shear_stress - 剪切应力 */
/* */ 磅/平方英寸 */
/* */
****************************************************************/
```

```c
#include <stdio.h>

int main()
{
    const float PI = 3.141593;
    int diameter, torsion_load, length_offset;
    float shear_stress;
    int page = 0;

    for(diameter = 5; diameter < 7; diameter++) {
        page = page + 1;
        printf("%d\n", diameter);
        printf("nTorsion load is: %d\n", torsion_load);
        printf("\n Length Offset %d\n", length_offset);
        printf(" Shear Stress%2f\n", shear_stress);

        /* 扭剪切应力的计算 */
        for(length_offset = 10; length_offset <= 20; length_offset += 5) {
            shear_stress = (16.0 * torsion_load * length_offset) / (PI * diameter * diameter);
            printf("%d\n", length_offset);
            printf("%8.2f\n", shear_stress);
        }
    }
    return 0;
}
```

输出

# 棒的直径: 5

扭负载是: 10000

| 长度偏移 | 扭剪切应力 |
| :--- | :--- |
| 10 | 4074.37 |
| 15 | 6111.55 |
| 20 | 8148.73 |

扭负载是: 12000

| 长度偏移 | 扭剪切应力 |
| :--- | :--- |
| 10 | 4889.24 |
| 15 | 7333.86 |
| 20 | 9778.48 |

# 棒的直径: 6

扭负载是: 10000

| 长度偏移 | 扭剪切应力 |
| :--- | :--- |
| 10 | 2357.85 |
| 15 | 3536.78 |
| 20 | 4715.70 |

## 248 控制结构

扭负载是: 12000

| 长度偏移 | 扭剪切应力 |
| :--- | :--- |
| 10 | 2829.42 |
| 15 | 4244.13 |
| 20 | 5658.84 |

## 4.5.4 摆的周期

问题：编写一个程序，计算单摆的周期，摆长从 2 英寸开始直到周期小于或等于 3.45。此程序使用限制控制。

数据 摆长 L（单位：英尺）从 1 开始变化。

方法 计算周期的公式为

$T = 2\pi\sqrt{\frac{L}{g}}$

其中 $g = 32.2$ 英尺/秒。

$T$ 是摆的周期（单位：秒）。$L$ 是摆的长度（单位：英尺）。

伪代码

```
L $\leftarrow$ 1
计算周期
当周期 $\le$ 3.45
    计算周期
    输出长度和周期
    L = L + 1
停止
```

# 程序

```c
****************************************************************/
/* */
/* 打印摆长和周期表 */
/* */
****************************************************************/
/* */ 常量: */
/* */
/* PI = 3.141593 */
/* */
/* GRAVITY = 32.2 英尺/秒 */
/* */
/* 输入变量: */
/* */
/* length - 摆长（英尺） */
/* */
/* 计算变量: */
/* */
/* period - 摆的周期（单位：秒） */
/* */ constant - 2*PI *
/* */
/* 输出变量: */
/* */
/* period - 摆的周期（单位：秒） */
****************************************************************/
```

```c
#include <stdio.h>
#include <math.h>

int main()
{
    FILE *outptr;
    const float GRAVITY = 32.2;
    const float PI = 3.141593;
    float length, period, constant;

    outptr = fopen("pend.dat", "w");

    constant = 2.0 * PI;
    length = 1.0;
    period = constant * sqrt(length / GRAVITY);
    fprintf(outptr, "OUTPUT\n");
    fprintf(outptr, "length\n");

    while(period <= 3.45)
    {
        fprintf(outptr,"%2.0f,      5.2f\n", length, period);
        length += 1.0;
        period = constant * sqrt(length / GRAVITY);
    }
    return 0;
}
```

| 长度 | 周期 |
| :--- | :--- |
| 1 | 1.11 |
| 2 | 1.57 |
| 3 | 1.92 |
| 4 | 2.21 |
| 5 | 2.48 |
| 6 | 2.71 |
| 7 | 2.93 |
| 8 | 3.13 |
| 9 | 3.32 |

## 4.5.5 钢棒的压缩应力和应变

问题：编写一个程序，计算钢棒的应力和应变，直径 D 从 2 英寸到 5 英寸，步长为 1.0，承受的压缩负载 P 从 50,000 到 100,000 磅/平方英寸，步长为 25,000。钢的弹性模量 $Es$ 为 $30 \times 10^6$ 磅/平方英寸。此程序使用嵌套循环并将输出写入文件。

方法 压缩应力通过公式计算：

```
$\sigma_c = \frac{P}{area}$
```

其中 $\sigma_c$ = 压缩应力（单位：磅/平方英寸）
$P$ = 压缩负载
area = 钢棒的截面积，公式为

```
$\frac{\pi d^2}{4}$
```

$d$ = 钢棒的直径。

压缩应变通过公式计算：

```
$\varepsilon = \frac{\sigma_c}{Es}$
```

其中 $\sigma_c$ = 压缩应力（单位：磅/平方英寸）
$\varepsilon$ = 应变（无量纲）
$Es$ = 钢的弹性模量（单位：磅/平方英寸）

数据 负载的 50,000、75,000 和 100,000 磅的实值。
直径 2.0、3.0、4.0 和 5.0 英寸的实值。

伪代码

```
对于每个负载
    输出带标签的负载
    对于每个直径
        area <- (3.141593 * d * d) / 4.0
        stress <- p / area
        strain <- stress / Es

        输出直径、应力和应变
    结束循环
结束循环
停止
```

# 程序

```c
****************************************************************/
/* 压缩负载下钢棒的 */
/* 应力和应变 */
****************************************************************/
/* */ 常量: */
/* */ PI = 3.141593 */
/* */ ES = 30000000 */
/* */ 输入变量: */
/* */ load -- 压缩负载（磅） */
/* */ diameter -- 钢棒的直径（英寸） */
/* */ 工作变量: */
/* */ area -- 截面积（平方英寸） */
/* */
/* 计算变量: */
/* */ stress - 压缩应力（磅/平方英寸 */
/* */ strain - 无量纲 */
/* */
/* 输出变量: */
/* */ load -- 压缩负载（磅） */
/* */ diameter -- 钢棒的直径（英寸） */
/* */ stress - 压缩应力（磅/平方英寸 */
/* */ strain - 无量纲 */
****************************************************************
```

```c
#include <stdio.h>
FILE *outptr;

int main ()
{
    const float PI = 3.141593;
    const float ES = 30000000;
    float load, diameter, area, stress, strain;

    outptr = fopen("fileout.dat", "w");

    for(load = 50000; load <= 100000; load += 25000)
    {
        fprintf(outptr,"\nCompression Load = %10.2f\n\n", load);
        fprintf(outptr,"Diameter      Stress      Strain\n");
        for(diameter = 2.0; diameter <= 5.0; diameter += 1.0)
        {
            area = (PI * diameter * diameter) / 4.0;
            stress = load / area;
            strain = stress / ES;
            fprintf(outptr,"%5.2f      %8.2f      %8.6f\n", diameter, stress, strain);
        }
    }
    return 0;
}
```

