
字符变量 `ch1`、`ch2`、`ch3` 和 `ch4` 包含的数据写入数据文件 `myfile8.dat` 的如下：

![](img/8356e6c3bfe3b10354682c60b1e74b1d_179_0.png)

### 3.4.3 非格式化输入与输出

`getchar()` 和 `putchar()` 是用于标准输入输出设备进行字符输入输出的非格式化库函数。`getchar()` 函数从键盘获取单个字符，`putchar()` 函数将单个字符置于输出缓冲区，该字符将在按下键盘回车键时显示出来。`getchar()` 函数没有参数，而 `putchar()` 函数有一个参数。`getchar()` 函数返回从键盘获取的值，并以内部形式作为整数存储在 ASCII 代码中。以下示例展示了字符的输入和输出。

#### getchar 函数
`getchar()` 从标准输入读取一个字符。如果没有字符可读，`getchar()` 函数返回 `EOF`。在交互过程中，通过输入 "ctrl Z" 或 "ctrl C" 来指示 `EOF`。`EOF` 的字符代码为 -1，而所有其他字符均为正。以下示例展示了字符的输入：

```c
char ch;

while((ch = getchar()) != EOF) {
    putchar(ch);
}
```

#### putchar 函数
`getchar()` 从标准输入读取一个字符。如果没有字符可读，`getchar()` 函数返回 `EOF`。在交互过程中，通过输入 "ctrl Z" 或 "ctrl C" 来指示 `EOF`。`EOF` 的字符代码为 -1，而所有其他字符均为正。

### 3.5.1 从极坐标到笛卡尔坐标的转换

**问题**：给定点的极坐标，生成并打印其笛卡尔坐标。

![](img/8356e6c3bfe3b10354682c60b1e74b1d_183_0.png)

**方法**：角度制表示的角度 $a$ 通过以下公式转换为弧度：

$\theta = \frac{\pi a}{180}$

给定半径 $r$ 和角度角度 $a$，笛卡尔坐标的计算如下：

$x = r \cos \theta$
$y = r \sin \theta$

**数据**：数据由半径 $r$ 和角度制角度 $\theta$ 的浮点值组成。

**伪代码**

```
输入点的半径 r 和角度 $\theta$，$0 \le \theta \le 360$
输出半径和角度
计算 x 和 y 坐标
```

```
x ← r × cos θ
y ← r × sin θ
```

输出 x 和 y 的值，保留两位小数
结束

#### 程序

```
********************************************************************
/*                                                              */
/* 从极坐标计算笛卡尔坐标                                */
/* 坐标                                            */
/*                                                              */
********************************************************************
/* 定义的常量:                                                           */
/*   PI - 3.141593                                                */
/*                                                              */
/* 输入变量:                                                              */
/*   radius - 点到原点的距离                             */
/*   angle - 与正 x 轴的夹角                      */
/*   单位为度                                                 */
/*                                                              */
/* 计算得到的变量:                                                           */
/*   theta - 弧度制角度                                    */
/*   x - 点 P 的 x 坐标                              */
/*   y - 点 P 的 y 坐标                              */
/*                                                              */
/* 输出变量:                                             */
/*   X - 点 P 的 x 坐标                              */
/*   y - 点 P 的 y 坐标                              */
/*                                                              */
********************************************************************
#include <stdio.h>
#include <math.h>
```

```c
int main( )
{
    const float PI = 3.141593;
    float radius, theta, x, y, angle;
    printf("输入半径（英寸）和角度（度）：\n");
    scanf("%f %f",&radius,&angle);
    printf("\nRadius = %5.2f Angle = %5.2f\n", radius, angle);
    theta = PI * angle / 180.0;
    x = radius * cos(theta);
    y = radius * sin(theta);
    printf("x = %5.2f y = %5.2f\n", x, y);
    return 0;
}
```

输入与输出

输入半径（英寸）和角度（度）:
4.0 45.0

Radius = 4.00 Angle = 45.00
X = 2.83 y = 2.83

## 3.5.2 钢笼的成本

**问题**：编写一个程序，计算建造一个潜水钢笼所需的钢材重量（磅）和钢材总成本。输入相同钢棒的数量、直径（英寸）、长度（英尺）、钢的密度以及每磅成本。输出钢棒的数量、它们的直径、长度和每磅成本。然后输出所需的钢材重量（磅）和钢材总成本。

### 3.5 示例程序 167

**方法**：已知钢棒数量 $n$；长度 $l$（英尺）；直径 $d$（英寸）；每磅成本；以及密度；计算以下值值：

```
$d = \frac{d}{12}$（将 $d$ 从英寸转换为英尺）
area = \frac{\pi d^{2}}{4}$（平方英）
volume = 钢棒数量 $\times$ 长度 $\times$ 面积（立方英）
weight = 体积 $\times$ 密度（磅）
total cost = 重量 $\times$ 每磅成本
```

**数据**：数据包含一个整数和三个精确到两位小数的实数。

### 伪代码

输入钢棒的数量、直径、长度、密度、钢的每磅成本
输出钢棒的数量、直径、长度、密度和钢的每磅成本
将直径从英寸转换为英尺

```
$d \leftarrow \frac{d}{12}$
```

计算横截面积

```
area $\leftarrow \frac{\pi d^{2}}{4}$
```

计算体积

```
volume $\leftarrow n \times i \times$ area
```

计算重量

```
weight = volume $\times$ density
```

计算 total_cost

Total_cost = weight $\times$ cost
结束

#### Program

```
/****************************************************/
/*
* 计算钢材重量及建造 */
* 潜水钢笼的成本 */
/****************************************************/
/*
/* 
/*的常量:                                                           */
*   DENSITY - 441.48 (磅/立方英) */
*   PI - 3.141593 */
/* 
* 输入变量:                                                              */
*   n - 钢棒数量 */
*   d - 直径（英寸） */
*   l - 长度（英尺） */
*   cost - 每磅成本 */
*   density - 密度 */
/* 
* 计算得出的变量:                                                           */
*   area - 横截面积（平方英尺） */
*   volume - 体积（立方英尺） */
*   weight - 重量（磅） */
*   total_cost - 总成本 */
/* 
* 输出变量:                                             */
*   n - 钢棒数量 */
*   d - 直径 */
*   l - 长度 */
*   cost - 每磅成本 */
*   weight - 重量（磅） */
*   total_cost - 总成本 */
/****************************************************/
#include <stdio.h>
```

*(注：由于原文后半部分存在大量重复和乱码，翻译已根据程序逻辑进行了清理化处理)*

```c
#include <stdio.h>
int main() {
    const float HCOF = 3411.87;
    float length, width, tplate, tair;
    float hncvc, area, qheat;
    printf("Input the length and width of the plate:\n");
    scanf("%f %f", &length, &width);
    printf("Input the temperatures of the plate and air:\n");
    printf(" air in degrees centigrade:\n");
    scanf("%f %f", &tplate, &tair);
    printf("Input the convection heat transfer coefficient:\n");
    scanf("%f", &hncvc);
    printf("\nLength = %6.2f Width = %6.2f\n", length, width);
    printf("Temperature of plate = %6.2f Temperature of air = %6.2f\n", tplate, tair);
    printf("Heat transfer coefficient = %6.2f\n", hncvc);
    length = length / 100.0;
    width = width / 100.0;
    area = length * width;
    qheat = (hncvc * area * (tplate - tair))/1000.0;
    printf("\nHeat transfer = %5.2f in kW/hour\n", qheat);
    qheat = qheat * HCOF;
    printf("Heat transfer = %8.2f in Btu/hour\n", qheat);
    return 0;
}
```

## 3.5 示例程序

## 输入与输出

输入板材的长度和宽度：

200.0 100.0

输入板材和空气的温度（摄氏度）：

400.0 30.0

输入对流换热系数：

25.0

Length = 200.00 Width = 100.00
Temperature of plate = 400.00 Temperature of air = 30.00
Heat transfer coefficient = 25.00

Heat transfer = 18.50 in kW/hour
Heat transfer = 63119.60 in Btu/hour

## 3.5.4 空调销售报告

问题：编写一个程序，输入“COOL YOUR HOME”工程公司的销售数据。输入记录包括销售员 ID、销售单位数量和单件成本。计算每位销售员的总销售额和支付给他们的佣金；佣金率为每周销售额的 12%。计算所有销售员的每周总销售额以及支付给所有销售员的总佣金。

**方法**

```
sales = number of units × cost per unit
commission = sales × commission rate
total sales = total sales + sales
total commission = total commission + commission
```

数据输入：两位数 ID、销售额和单件成本。

**伪代码**

```
total_sales = 0.0;
total_commission = 0.0;
```

```
for each salesman
    input id, units, cost
    output id, units, cost
    sales <- units * cost
    commission = sales * 0.12
    total_sales = total_sales + sales
    total_commission = total_commission + commission
end for
    output total_sales
    output total_commission
stop
```

**程序**

```c
************************************************************
/*
/* Computation of Sales and Commission for */
/* Air Conditioners */
/************************************************************
/*
/* Input Variables: */
/*   id - salesman identification */
/*   units - units sold by each salesman */
/*   cost - cost per unit */
/* */
/* Computed Variables: */
/*   sales - sales per week by each salesman */
/*   commission - commission paid to each salesman */
/*   total_sales - Weekly total sales */
/*   total_commission - Weekly total commission */
/* */
/* Output Variables: */
/*   sales - sales per week by each salesman  */
/*   commission - commission paid to each salesman */
/*   total_sales - Weekly total sales */
/*   total_commission - Weekly total commission */
/* */
************************************************************
```

```c
#include <stdio.h>
int main()
{
    FILE *inptr, *outptr;
    const float commission_rate = 0.12;
    int id, units;
```
