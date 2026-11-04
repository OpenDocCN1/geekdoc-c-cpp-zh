
```c
for(k = 0; k < 5; k++)
{
    printf("%s\n", names[k]);
}

return 0;
}
```

图 3.65 程序 apointers.c

### 示例 3.38

编写一个程序来展示如何使用指针数组。

### 解决方案 3.38

图 3.66 显示了程序清单（程序：apointers2.c）。在此程序中，名为 **numbers** 的数组被初始化为 5 个整数。指针 **ptr** 被声明为包含 5 个元素。创建了一个 **for** 循环，并将指针元素设置为指向数组元素的地址。另一个 **for** 循环用于显示数组元素的内容。程序显示以下输出：

```text
numbers[0] = 10
numbers[1] = 20
numbers[2] = 30
numbers[3] = 40
numbers[4] = 50
```

```c
/***********************************************
              ARRAY OF POINTERS
              ==================
This program is an example of array of pointers

Author: Dogan Ibrahim
File : apointers2.c
Date : December 2020
***********************************************/

#include <stdio.h>

#define max 5

int main(void)
{
    int numbers[max] = {10, 20, 30, 40, 50};
    int *ptr[max];
    int k;

    for(k = 0; k < max; k++) ptr[k] = &numbers[k];

    for(k = 0; k < max; k++) printf("numbers[%d] = %d\n", k, *ptr[k]);

    return 0;
}
```

图 3.66 程序 apointers2.c

### 函数指针

函数指针用于指向函数而不是数据。它们可用于菜单型应用程序中。下面给出了一个示例。

### 示例 3.39

编写一个程序对两个数字进行操作。所需操作为：加、减、乘和除。在你的程序中使用函数指针作为 MENU。

### 解决方案 3.39

所需的程序清单显示在图 3.67 中（程序：**apointers3.c**）。在程序开始时，创建了一个名为 **ptr** 的函数指针，指向函数 **Add**、**Subtract**、**Multiply** 和 **Divide**。提示用户输入两个数字，以空格分隔。使用四个函数进行加法、减法、乘法和除法运算。然后创建一个包含四个选项的 MENU，并要求用户输入选择。然后根据用户的选择使用函数指针调用相应的函数。

```c
/*----------------------------------------------------
                    FUNCTION POINTERS
                    =================

This program is an example of using function pointers

Author: Dogan Ibrahim
File  : apointers3.c
Date  : December 2020
----------------------------------------------------*/
#include <stdio.h>

void Add(float a, float b)
{
    printf("\nThe sum is: %f\n", a + b);
}

void Subtract(float a, float b)
{
    printf("\nThe difference is: %f\n", a - b);
}

void Multiply(float a, float b)
{
    printf("\nThe product is: %f\n", a * b);
}

void Divide(float a, float b)
{
    printf("\nThe division is: %f\n", a / b);
}

int main(void)
{
    float x, y;
    void (*ptr[])(float, float) = {Add,Subtract,Multiply,Divide};
    int choice;

    printf("\nEnter two numbers: ");
    scanf("%f %f", &x, &y);

    printf("\n   MENU\n");
    printf("  =====\n");
    printf("0: Add\n");
    printf("1: Subtract\n");
    printf("2: Multiply\n");
    printf("3: Divide\n");
    printf("\n   Choice?: ");
    scanf("%d", &choice);

    (*ptr[choice])(x, y);

    return 0;
}
```

图 3.67 程序 apointers3.c

程序的示例运行显示在图 3.68 中。

```text
Enter two numbers: 12 4

MENU
====
0: Add
1: Subtract
2: Multiply
3: Divide

Choice?: 2

The product is: 48.000000
```

图 3.68 程序运行示例

### 3.3 • 摘要

在本章中，我们学习了 C 的基本编程特性。不熟悉 C 的读者可以参考互联网上提供的许多文章、书籍和教程。

在下一章中，我们将了解使用 C 编程 Raspberry Pi 的不同方法。

## 第 4 章 • 使用 C 进行硬件编程

### 4.1 • 概述

本书的主要主题是使用 C 语言在 Raspberry Pi 上开发项目。有几种 C 编译器可与 Raspberry Pi 一起使用。在本章中，我们将通过开发一个非常简单的项目来简要介绍这些编译器。在本书的剩余章节中，所选编译器将用于开发各种基于硬件的项目。

### 4.2 • 通用输入输出端口（GPIO）

在深入了解 C 编译器和硬件接口的细节之前，值得先了解一下 Raspberry Pi 4 的 GPIO 连接器。如图 4.1 所示，该连接器是一个 40 引脚、双列直插、宽 2.54mm 的连接器。其他最近的 Raspberry Pi 型号具有类似的连接器，引脚配置几乎相同。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_99_0.png)

图 4.1 Raspberry Pi 4 GPIO 连接器

当 GPIO 连接器位于电路板的远端时，从连接器左侧开始，底部引脚编号为 1、3、5、7，依此类推。顶部引脚编号为 2、4、6、8，依此类推。

GPIO 提供 26 个通用双向 I/O 引脚。其中一些引脚具有多重功能。例如，引脚 3 和 5 分别是 GPIO2 和 GPIO3 输入输出引脚。这些引脚也可分别用作 I2C 总线、I2C SDA 和 I2C SCL 引脚。同样，引脚 9、10、11、19 可用作通用输入输出，或用作 SPI 总线引脚。引脚 8 和 10 保留用于 UART 串行通信。

提供了两个电源输出：+3.3V 和 +5.0V。GPIO 引脚在 +3.3V 逻辑电平下工作（不像许多其他以 +5V 工作计算机电路）。引脚可以是输入或输出。配置为输出时，引脚电压为 0V（逻辑 0）或 +3.3V（逻辑 1）。Raspberry Pi 4 通常使用外部电源（例如市电适配器）供电，输出为 +5V，电流容量至少为 2A。3.3V 输出引脚可提供高达 16mA 的电流。所有输出引脚的总电流不应超过 51mA 的限制。连接外部设备到 GPIO 引脚时应小心，因为抽取过大电流或引脚短路很容易损坏你的 Pi。5V 引脚可提供的电流取决于许多因素，例如 Pi 本身所需的电流、USB 外设消耗的电流、摄像头电流、HDMI 端口电流等。

配置为输入时，高于 +1.7V 的电压将被视为逻辑 1，低于 +1.7V 的电压将被视为逻辑 0。应注意不要向任何 I/O 引脚提供大于 +3.3V 的电压，因为大电压很容易损坏你的 Pi。例如，Arduino 的输出引脚不得直接连接到 Raspberry Pi 输入引脚，否则很容易损坏输入电路。同样，虽然将 Raspberry Pi 输出引脚连接到 Arduino 输入引脚是安全的，但当 Raspberry Pi 处于逻辑 1 时，其输出电压电平可能不足以驱动 Arduino 输入电路。在这种情况下，应使用电压电平转换电路将 5V 转换为 3.3V 逻辑电平，或将 3.3V 转换为 5V。图 4.2 显示了一个示例电压电平转换电路。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_100_0.png)

图 4.2 电压电平转换电路

### 4.3 • 与 GPIO 接口

#### 4.3.1 • 需要小电流的负载

需要小电流的负载（如 LED）可通过限流电阻直接连接到 GPIO 引脚。LED 有不同尺寸。小型 LED 消耗几毫安电流，而较大 LED 需要约 15mA 才能明亮。LED 上的压降再次取决于所用 LED 的类型。在大多数情况下，我们可以假设压降约为 2V。LED 可以按如下所述以电流源或电流汇模式连接。

currents, while MOSFET transistors are more suitable for higher currents.

图 4.5 显示了一个双极晶体管开关，负载连接到集电极电路。这里，当晶体管导通时，负载被激活，即当 Raspberry Pi 的输出为逻辑 1 时（即晶体管被导通时）。1K 基极电阻适用于大多数应用。如果负载是感性的，应如 图 4.6 所示使用二极管以保护晶体管免受反电动势影响。

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_102_0.png)

图 4.5 使用双极晶体管

![](img/7ba4e9a445f8a2ad48358a7aed37b32e_102_1.png)

图 4.6 使用感性负载

图 4.7 显示了一个基于 MOSFET 的电路，适用于较大电流，通常在数百毫安范围内。同样，当 Raspberry Pi 的输出为逻辑 1 时，负载被激活。
