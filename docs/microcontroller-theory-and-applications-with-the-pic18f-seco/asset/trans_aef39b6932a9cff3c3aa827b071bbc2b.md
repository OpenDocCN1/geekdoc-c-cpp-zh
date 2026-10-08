
而 A-F 将按图 9.20 所示正确显示。例如，如果按下键 ‘F’，则所有 LED 段都会关闭。

以下是 PIC18F4321 键盘接口的 C 语言程序：

```c
#include <P18F4321.h>
#define TRUE 1
#define FALSE 0
#define setbit(var,bit)((var) |= (1<<bit))    // #1 set a bit var = var | (1 <<bit)
#define clearbit(var,bit)((var) &= ~(1<<bit)) // #2 clear a bit var = var & ~(1<<bit)
#define testbit(var,bit)((var) & (1<<bit))  // #3 test a bit return var & (1<<bit)

unsigned char row = 0x0F;                     // #4 all rows are initially high
int i = 0, j = 0;
unsigned char Matrix[4][4] =                  // #5 create a matrix to store the
                                              // corresponding Hex key numbers
{
    {0x0F, 0x0E, 0x0D, 0x0C},
    {0x0B, 0x0A, 0x09, 0x08},
    {0x07, 0x06, 0x05, 0x04},
    {0x03, 0x02, 0x01, 0x00}
};
void delay_ms(unsigned int time);             // #6 delay function to provide 2ms delay

void main()
{
    OSCCON = 0x60;                            // 4MHz clock
    AICON1 = 0x0F;                            // #8 AN0-AN12 all digital input
    TRISB = 0x00;                             // #9 configure PORTB as output for 7 seg decoder
    TRISC = 0x00;                             // #10 configure PORTC as output for matrix keyboard
    TRISD = 0x0F;                             // #11 configure PORTD as input for key pressed
    PORTB = 0x00;                             // #12 output initially set to 0 at PORTB

    while (1) {
        PORTC = 0x00;                         // #13 output initially set to 0 at PORTC
        while(PORTD != 0x0F);                 // #14 wait in while loop if a key is pressed
        while(PORTD == 0x0F);                 // #15 wait in while loop if no keys are pressed

        for(i = 0; i < 4; i++)               // #16 Scan for the keyboard FOR COLUMN
        {
            for(j = 0; j < 4; j++)            // #17 Scan FOR ROWS
            {
                clearbit(row, j);             // #18 Clear a bit for corresponding row j
                PORTC = row;                 // #19 Output a low for that row

                if(testbit(PORTD, i) == 0)    // #20 Detect if a key is pressed in column i
                {
                    delay_ms(20);             // #21 Delay for 20ms
                    if(testbit(PORTD, i) == 0) // #22 Check again for debouncing
                    {
                        PORTB = Matrix[j][i];  // #23 output result from lookup table to PORTB
                    }
                }
                setbit(row, j);               // #24 Set the zero bits back to row variable
            }
        }
    }
}

void delay_ms(unsigned int time)              // #25 2ms delay function
{
    unsigned int i, j;
    for(i = 0; i < time; i++)
        for(j = 0; j < 255; j++);
}
```

在图 9.21 中，十六进制键盘的四行四列分别通过 PORTC 和 PORTD 连接到 PIC18F4321。键盘的最上面一行（第 0 行）连接到 RC0，下一行（第 1 行）连接到 RC1，再下一行（第 2 行）连接到 RC2，最后一行（第 3 行）连接到 RC3。另一方面，最右边的一列（第 0 列）连接到 RD3，向左的下一列（第 1 列）连接到 RD2，再向左的下一列（第 2 列）连接到 RD1，最后向左的一列（第 3 列）连接到 RD0。在图中，连接到 +5V 的键盘列通常处于高电平。程序第 #5 行中的键矩阵排列方式与图 9.21 中的键盘不同。例如，在程序中，键 ‘F’ 位于第 0 行第 0 列。因此，键 ‘F’ 位于键矩阵最右端的顶行。

为了检测按键操作，使用 “PORTC = 0x00;”（第 #13 行）在四行上输出 0。如果按下某个键，该键会使其连接的通常处于高电平的列变为 ‘0’。因此，按下的键会使与其连接的某一列变为 ‘0’，而其他三列将保持高电平。

第 #18 行清除第 j 行的一位，第 #19 行在该行上输出低电平。第 #20 行检测与该行连接的第 i 列中是否有键被按下。一旦找到按键，就会进行消抖处理（第 #21 行）。利用 i 和 j，从键矩阵 [j][i] 中获取按键，然后输出到七段数码管的 PORTB（第 #23 行）。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_277_0.png)

### 图 9.21
PIC18F4321 与键盘和显示的接口，用于 C 程序

举个例子，考虑按下数字键 2。注意 ‘2’ 位于第 3 行（j = 3）和第 1 列（i = 1）。在程序中，j 和 i 的初始值均为 0。“clearbit” 函数（第 #18 行）清除一个位，然后 “PORTC = row;”（第 #19 行）在该行上输出 ‘0’。这意味着当 j = 0 且 i = 0 时，PORTC 输出 0xE (1110)。“testbit” 函数（第 #20 行）检查 PORTD 的输入是否为 0。如果为 0，则找到了按键。对该按键进行消抖（第 #21 行），然后输出到 PORTB。因此，按下的键将显示在七段数码管上。对于按下的键 ‘2’，此时尚未找到该键。因此，过程将继续，直到 j = 3 且 i = 1。

当 j = 3 且 i = 1 时，第 #18 行的 “clearbit” 函数清除第 3 行（j = 3）的一个位，并在 PORTC 的低四位输出 0x7 (0111)。当执行带有 “testbit” 函数的 “if” 语句时（第 #20 行），得到第 1 列（i = 1）。坐标 j = 3（第 3 行）和 i = 1（第 1 列）提供了被按下的键 ‘2’。然后对该按键进行消抖并输出到 PORTB。因此，七段数码管将显示 ‘2’。

## 习题与问题

- 9.1 上电复位时的中断地址向量是什么？

- 9.2 识别 PIC18F4321 的外部中断是可屏蔽的还是不可屏蔽的。

- 9.3 高优先级和低优先级中断的中断地址向量是什么？

- 9.4 PIC18F4321 的 INT0 至 INT2 外部中断在上电复位时的优先级级别是什么？

- 9.5
  - (a) 使用 PIC18F 汇编语言编写指令序列，将 INT1 的中断优先级设置为高优先级，将 INT2 的中断优先级设置为低优先级。
  - (b) 编写 C 语言程序，将 INT1 的中断优先级设置为高优先级，将 INT2 的中断优先级设置为低优先级。

- 9.6 INT0 的中断优先级级别是什么？

- 9.7 INT0-INT2 在上电复位时的触发级别（上升沿或下降沿）是什么？编写一个 PIC18F 汇编语言程序，通过上升沿激活 INT0 的触发级别，并通过下降沿激活 INT1 和 INT2 的中断。

- 9.8 PIC18F4321 上提供了多少个变化中断（Interrupt-on-Change）引脚？它们是由上升沿还是下降沿触发的？

- 9.9 在图 P9.9 中，要求 PIC18F4321 在连接到 PORTC 第 0 位的比较器输出为 1（$V_x > V_y$）时，点亮连接到 PORTD 第 1 位的 LED；否则，关闭 LED。
  - (a) 在地址 0x200 处编写一个使用条件判断或轮询 I/O 的 PIC18F 汇编语言程序来实现此功能。
  - (b) 编写一个 C 语言程序来实现此功能。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_279_0.png)

**图 P9.9**

- 9.10
  - (a) 使用中断 I/O 重复问题 9.9，将比较器输出连接到 INT1。注意 RB1 也与 INT1 复用。使用 PIC18F 汇编语言在主程序 0x80 处编写主程序，在 0x150 处编写中断服务例程。主程序将配置 I/O 端口，启用中断 INT1，将 STKPTR 初始化为 0x10，关闭 LED，然后等待中断。中断服务例程将点亮 LED，并返回到主程序的适当位置，以便在下一个中断发生前 LED 持续点亮。
  - (b) 使用 C 语言重复 (a)，除了不需要初始化 STKPTR，且主程序和服务例程的起始地址也不需要指定。

- 9.11 在图 P9.11 中，如果 $V_M > 12$ V，点亮连接到 PORTA 第 3 位的 LED。如果 $V_M < 11$ V，关闭 LED。根据需要端口、寄存器和内存位置以及 INT0 中断：
  - (a) 绘制一个整洁的框图，显示 PIC18F4321 微控制器以及与图 P9.11 中所示端口连接的线路。
  - (b) 使用 PIC18F 汇编语言在 0x150 处编写主程序，在 0x200 处编写服务例程。主程序将初始化端口并等待中断。服务例程将完成任务并停止。
  - (c) 使用 C 语言重复 (b)。注意，主程序和服务例程的起始地址不像汇编语言中那样需要指定。

- 9.12 Hitachi HD44780 LCD 上 RS、R/W̄ 和 EN 引脚的目的是什么？简要描述这些信号如何通过 D0-D7 引脚在 LCD 上显示数据。

- 9.13 假设图 9.14 中的 PIC18F4321 - Hitachi HD44780 LCD 接口。
  - (a) 使用 PIC18F 汇编语言编写一个程序，当连接到 PORT C 的四个输入开关全部为高电平时，立即在 LCD 上显示短语 “PIC18F”。
  - (b) 使用 C 语言重复 (a)。

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_280_0.png)

**图 P9.11**

