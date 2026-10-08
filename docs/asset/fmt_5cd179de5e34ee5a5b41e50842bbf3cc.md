
```c
unsigned short dtime; // delay time

int ix;

const int numstates = 18; // index into states

const char seg7[] = {

    0x6D, 0x00, 0x6D, 0x00, 0x6D, 0x00 // S

    0x3F, 0x00, 0x3F, 0x00, 0x3F, 0x00 // O

    0x6D, 0x00, 0x6D, 0x00, 0x6D, 0x00 // S

};

const char delay[] = {

    0x0C, 0x00, 0x0C, 0x0C, 0x18, // dots

    0x24, 0x24, 0x24, 0x24, 0x24, // dashes

    0x0C, 0x00, 0x0C, 0x0C, 0x30 // dots

};

void interrupt 7 handler() {

    time--;

    if(dtime == 0) {

        seg7 on(seg7[ix],3); // turn on next display

        time = delay[ix]; // get next delay time

        ix++; // increment index

        if(ix == numstates) { // after going through all states

            ix = 0; // reset index to 0

        }

        clear_RTI_flag();

    }

}

void main(void) {

    PLL_init(); // set system clock frequency to 24 MHz

    led_disable(); // disable LEDs

    seg7_enable(); // enable 7-segment displays

    RTI_init();

    ix = 0; // reset index into states

    dtime = 1; // start display right away

    while (1) {

        // do nothing while display goes

    }

}
```

![](img/6c970885d6405944bd67e68f02bac5bc_82_0.png)

# 第 6 章

## 模数转换器

在本章中，我们将展示如何使用 MC9S12DG256 微控制器部分的两个 8 通道模数（A/D）转换器。我们将使用 A/D 转换器读取电位计值、读取 x-y-z 加速度计的值，并测量华氏度和摄氏度下的温度。

### 6.1 模数转换

A/D 转换器将给定电压范围内的模拟电压转换为相应的数字。例如，你可能将 0 到 5 伏之间的电压转换为 00000000 到 11111111 之间的 8 位二进制数。这代表了 0 到 255 之间的十进制数。在这种情况下，最低位（LSB）1 对应于 5V/256 = 19.5 mV 的电压变化。这种量化误差（或步长）是任何类型的 A/D 转换中固有的。我们可以使用更多的位来最小这种误差。例如，10 位 A/D 转换器在 0 到 5 伏之间的步长为 5V/1024 = 4.9 mV。MC9S12DG256 A/D 转换器可以编程为执行 8 位或 10 位转换。我们将提供用于 10 位转换的 C 函数。

执行 A/D 转换有多种不同的方法。最流行的方法之一（HC12 微控制器使用的方法）是逐次逼近法。我们将使用 4 位转换来说明这种方法，其在 0 到 5 伏之间的步长为 5V/16 = 0.3125 V。对于 n 位，逐次逼近法需要如图 6.1 所示的二分搜索。假设要转换的输入模拟电压为 $V_i = 3.5V$。逐次逼近的第一步是猜测中间范围电压 2.5V。即我们设置最高位。如果该电压（2.5V）小于 $V_i$，则我们保留该位。然后我们加上下一个最高位并尝试 1100，步骤2。此值大于 3.5V，所以我们过头了，必须放弃该位。设置下一位意味着尝试电压 1010，3.125V，步骤3。这小于 3.5V，我们保留该位。最后，我们将设置最后（最低）位并尝试 1011，3.475V，步骤4。这仍然小于 3.5V，因此我们保留该位。现在已完成，转换值为 1011，代表 3.475V，但在我们的 0.3125V 误差范围内。

### 图 6.1 逐次逼近法说明

| 步骤 | 二进制 | 电压 |
| --- | --- | --- |
| 1 | 1000 | 2.5V |
| 2 | 1100 | 3.75V |
| 3 | 1010 | 3.125V |
| 4 | 1011 | 3.475V |

图 6.1 所示的逐次逼近法可以使用图 6.2 所示的比较器和 D/A 转换器实现。假设如图 6.1 所示的4 位 A/D 转换器，电路首先输出二进制值 1000。D/A 转换器将此值转换为 $V_{DA} = 2.5V$。由于此值小于 $V_{in} = 3.5V$，比较器的输出 $C$ 将为 1。这告诉电路保留该位并在第二个步骤输出值 1100。此时 $V_{DA} = 3.75V$ 大于 $V_{in} = 3.5V$，因此比较器的输出 $C$ 将为 0。这告诉电路丢弃该位并在步骤 3 输出值 1010。该位如图 6.1 所示作为最后一位保留。

![](img/6c970885d6405944bd67e68f02bac5bc_84_0.png)

### 图 6.2 实现逐次逼近法

### 6.2 使用 MC9S12DG256 A/D 转换器

MC9S12DG256 微控制器有两个 A/D 转换器，称为 ATD0 和 ATD1，可以产生 8 位或 10 位转换。这些 A/D 转换器与 PORTAD0 和 PORTAD1 通用引脚，当未使用 A/D 转换时可用于数字输入。PORTAD0 的引脚 7 连接到 DRAGON12-Plus-USB 板上的电位计中心。当用小螺丝刀转动电位计时，该输入会在 0 到 5 之间变化。我们将使用此输入来说明 ATD0 的输出。

有很多与 A/D 转换器使用相关的寄存器。我们将在下面的“内部”部分查看它们。为了方便，我们编写了表 6.1 中 C 函数调用的汇编程序。

表 6.2 显示了两个 A/D 转换器的引脚分配。在 DR12-Plus-USB 上，ATD0 的通道 7 连接到电位计，ATD0 的通道 5 连接到温度传感器，ATD0 的通道 4 连接到光敏极。DRAGON12-Plus-USB 有一个 10 脚接头连接到 ATD1 通道 0-2 的输出。此接头方便将 x-y-z 加速度计或 GP2D12 传感器连接到 MC9S12DG256 微控制器的 A/D 通道。

### 表 6.1 A/D 转换器的 C 函数

| 函数 | 说明 |
| --- | --- |
| `void ad0enable(void);` | 开启 10 位 ATD0 |
| `int ad0conv(char#);` | 返回通道# 四次连续读取的平均值 |
| `void ad1enable(void);` | 开启 10 位 ATD1 |
| `int ad1conv(char#);` | 返回通道# 四次连续读取的平均值 |

### 表 6.2 A/D 转换器引脚分配

| 通道号 | 引脚名称 | 引脚号 | 通道号 | 引脚名称 | 引脚号 |
| --- | --- | --- | --- | --- | --- |
| 0 | PADD0 | 67 | 0 | PADD8 | 68 |
| 1 | PADD1 | 69 | 1 | PADD9 | 70 |
| 2 | PADD2 | 71 | 2 | PADD10 | 72 |
| 3 | PADD3 | 73 | 3 | PADD11 | 74 |
| 4 | PADD4 | 75 | 4 | PADD12 | 76 |
| 5 | PADD5 | 77 | 5 | PADD13 | 78 |
| 6 | PADD6 | 79 | 6 | PADD14 | 80 |
| 7 | PADD7 | 81 | 7 | PADD15 | 82 |

### 示例 17 – 读取电位器值

列表 6.1 显示了一个程序，该程序读取 ATDO 的通道 7，将值除以 2（以降低最低位的噪声），并将结果显示在 LCD 屏幕上。当你用小螺丝刀旋转电位器时，数值会在 0 到 511 之间变化。尝试一下。

在 DRAGON12-Plus-USB 上，如果你将列表 6.1 中的通道号从 7 改为 4，程序将读取板载光电极管的输出。当你向光电极管照射更多的光时，LCD 上的显示数值将会增加。

### 列表 6.1 示例 17

```c
// Example 17: A/D Converter -- Pot

#include <stdio.h>      /* 通用定义和宏 */

#include <mc9s1dg256.h>   /* 变体信息 */

#pragma LINK_INFO_DERIVATIVE mc9s1dg256b

#include "main_asm.h"      /* 与汇编模块的接口 */

int val;

void main(void) {

    PLL init();             // 设置系统时钟频率为 24 MHz

    ad0_enable();          // 启用 a/d 转换0

    lcd_init();             // 启用 led

    while(1) {

        val = adconv(7);     // 读取通道7 上的电位器

        val = val >> 1;      // 右移 1 位（除以 2）

        set_lcd_addr(0x40);  // 显示在 LCD 的第二行

        write_int_lcd(val);  // 将值写入第5个字段

        ms_delay(100);      // 延迟 0.1 秒

    }

}
```

### 底层原理

main.asm 中对应表 6.1 所示 C 函数的子程序见列表 6.2。前三个子程序适用于 ATDO，后三个子程序适用于 ATD1。子程序 `ad0_enable` 将启用 ATDO 的 10 位分辨率模式。A/D 时钟频率可以在 500 kHz 到 2 MHz 之间。它使用图 6.3 中 ATD 控制寄存器 4 中的位 [PRS4:0] 根据以下公式设置：

> `ATDclock = [BusClock] / 2^(PRS+1)` (6.1)

在列表 6.2 的子程序 `ad0_enable` 中，我们在控制寄存器 `ATDCTL4` 中存储了值 `0B`。将在 (6.1) 中使用 PRS=1，这将 24 MHz 的总线时钟频率除以 24，得到 1 MHz 的 A/D 时钟频率。在控制寄存器 `ATDCTL2` 中存储值 `SC` 将关闭 A/D 转换完成标志。此功能将在从相应的结果器读取数据时清除 A/D 转换完成标志。

### 列表 6.2 来自 main.asm 的 A/D 汇编子程序

```asm
; A/D converter PADD0-PADD7

; ad0_enable();

ad0_enable:

movb #$OB, ATDCT0L4      ;10位分辨率 /24时钟

movb #$CO, ATDCT0L2      ;设置 ADPU & AFFC

rts
```

```asm
; int adconv(char ch)

ad0conv:

andb #$07, ATDCT0L4      ;ch - 7

orb #$80, ATDCT0L5       ;SCAN=0

brclr ATDSTATO,$80,ad01  ;等待转换

ad01:

bsr

avg0:

psxh                    ;保存寄存器

ldx                    #ATD0H

addd 2,x;               +adr1

addd 2,x;               +adr2

addd 2,x;               +adr3

lsrd                    ;除以 4

pulx                    ;恢复寄存器

rts
```

```asm
; A/D converter PADD8-PADD15

; ad1_enable();

ad1_enable:

movb #$OB, ATDCT1L4      ;10位分辨率 /24时钟

movb #$CO, ATDCT1L2      ;设置 ADPU & AFFC

rts
```

```asm
; int adconv(char ch)

ad1conv:

andb #$07, ATDCT1L4      ;ch - 7

orb #$80, ATDCT1L5       ;SCAN=0

brclr ATDSTATO,$80,ad11  ;等待转换

ad11:

bsr

avg1:

psxh                    ;保存寄存器

ldx                    #ATD1H

addd 2,x;               +adr1

addd 2,x;               +adr2

addd 2,x;               +adr3

lsrd                    ;除以 4

pulx                    ;恢复寄存器

rts
```

## 模拟量转数字器

### ATD 控制寄存器 2 (ATD0CTL2–0082) (ATD1CTL2–0102)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| ADPU | AFFC | AWAI | ETRIG | ERIE | ASCIE | ASCIF | |
- ADPU = 1: 正常 ATD 功能；ADPU = 0: 掉。
- AFFC = 1: 启用 ATD 快标志；AFFC = 0: 清除 ATD 快标志。
- ASCIE = 1: 启用 ATD 序列中断；ASCIE = 0: 禁用序列中断。
- ASCIF: ATD 序列中断标志。

### ATD 控制寄存器 3 (ATD0CTL3–0083) (ATD1CTL3–0103)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| 0 | S8C | S4C | S2C | S1C | FIFO | FRZ1 | FRZ0 |
- S8C, S4C, S2C, S1C: 转换长度
- FIFO: 结果模式
- FRZ1, FRZ0: 调试启用

### ATD 控制寄存器 4 (ATD0CTL4–0084) (ATD1CTL4–0104)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| S0 | PRS1 | PRS2 | PRS3 | PRS4 | SMP0 | SRES | |
- SRES8 = 1: 8位分辨率；SRES8 = 0: 10位分辨率。
- SMP1, SMP0: 采样时间选择
- PRS[4:0]: ATD 分频

### ATD 控制寄存器 5 (ATD0CTL5–0085) (ATD1CTL5–0105)

| 7 | 6 | 5 | 4 | 3 | 2 | 1 | 0 |
|---|---|---|---|---|---|---|---|
| CH0 | CH1 | CH2 | MULT | SCAN | DSGN | DJM |
- DJM = 1: 结果寄存器右对齐数据
- DJM = 0: 结果寄存器左对齐数据
- DSGN = 1: 结果寄存器有符号数据
- DSGN = 0: 结果寄存器无符号数据
- SCAN = 1: 连续转换序列（扫描模式）
- SCAN = 0: 单次转换序列
- MULT = 1: 跨通道采样
- MULT = 0: 仅采样一个通道
- CH[2:0]: 模拟输入通道

![](img/6c970885d64059bd67e8f02bac5bc_88_0.png)

一旦启用转换模块，通过写入控制寄存器 `ATDCTL5` 开始转换。将位 7 (DJM) 设置为 1 将使结果寄存器数据右对齐。在位 5 (SCAN) 和位 4 (MULT) 中存储 0 将导致单通道转换序列。通道号存储在位 2–0 中。在子程序 `adconv` 中，通道号作为参数传递到累加器 B。通过对该数字进行掩码处理，将位 7 置为 1 以使结果寄存器数据右对齐，结果写入 `ATDCTL5`。转换开始。发生的转换次数由图 6.3 所示的 ATD 控制寄存器 3 中的转换长度值决定。重置时，该转换长度的默认值为 4，这意味着在我们的情况下，会对选定通道进行四次单独转换，结果存储在 ATD 控制寄存器（ATDRHx/ATDRlx）的前四个字中。

当转换完成后，图 6.4 所示的 ATD 状态寄存器 0 的位 7 (SCF) 被设置为 1。清除跳转语句

```
ad01    brclr ATDSTATO,$80,ad01
```
