
即使断电时仍可保留内容。这对于需要设置密码、存储校准数据或像日志功能那样存储数据测量的用户应用非常有用。25LC256 使用 SPI 接口与 Microstick II PIC24H 微控制器通信。在我们的实验中，我们使用一个软件 'C' 库，其中 SPI 通信得到支持，并提供易于使用的 API。

对于此库，每个 25LC256 存储字为两个字节。鉴于 25LC256 的字节大小，这意味着我们最多可以存储 16K 个字。总共。双字节存储和检索是有意义的，因为 PIC24H 是一款 16 位机器。一般来说，对于你的实验，你需要确定要存储的数据以及该数据如何在 16K 字上组织。图 8-3 显示了物理 EEPROM。它是一个 8 引脚 DIP。你已经可以识别基本 SPI 信号 /CS、SCK、SI 和 SO。此外，对于此 EEPROM，还有额外的控制信号。有写保护 (/WP) 控制线，可物理锁定微控制器对 EEPROM 的写入。/HOLD 暂停命令/数据序列，并将设备置于暂停状态，一旦 /HOLD 释放，无需重新启动序列。

- CS – 芯片选择
- SCK – 串行时钟
- SI – 串行输入
- SO – 串行输出
- WP – 写保护
- HOLD – 保持使能

![](img/a9229e7b0ddd9608f171b22b52514f39_150_0.png)

图 8-3：SPI EEPROM

## 实验 1- 硬件

PIC24H 具有用户可编程 PPS 引脚，可将任何内部数字外设的 I/O 放置到这些引脚中的任何一个。我们将配置引脚 18、17 和 16 以用作 SPI2 的接口，即 SO、CLK 和 SI。引脚 15 将配置为 /CS 的普通数字输出。/HOLD 和 /WP 不是必需的，因此接高以禁用。最终硬件原理图如图 8-4 所示。图 5、6、7 显示了 25LC256 EEPROM 指令集以及使用 SPI 的读/写字节序列。请注意，EEPROM 的所有地址都是 16 位的。当 /CS 变为活动状态时，微控制器首先向 EEPROM 发送特定命令（见图 8-5），然后是地址。接下来发生什么取决于命令是读操作还是写操作；如果是读操作，EEPROM 将向主设备输出数据以供读取，如果是写操作，主设备将向 EEPROM 输出数据以存储。大多数 EEPROM 通常不是高速设备，内存写入周期可能需要几毫秒。API 处理此事。

![](img/a9229e7b0ddd9608f171b22b52514f39_151_0.png)

+5V 外部电源或从 TP1 取电

图 8-4 原理图

| 指令名称 | 指令格式 | 描述 |
|---|---|---|
| READ | 0000 0011 | 从选定地址开始从存储器阵列读取数据 |
| WRITE | 0000 0010 | 从选定地址开始向存储器阵列写入数据 |
| WDI | 0000 0100 | 重置写使能锁存器（禁用写操作） |
| WREN | 0000 0110 | 设置写使能锁存器（使能写操作） |
| RDSR | 0000 0101 | 读取状态寄存器 |
| WRSR | 0000 0001 | 写入状态寄存器 |

图 8-5：Microchip 25LC256 EEPROM 指令集

![](img/a9229e7b0ddd9608f171b22b52514f39_152_0.png)

图 8-6：25LC256 EEPROM 字节读取序列

![](img/a9229e7b0ddd9608f171b22b52514f39_152_1.png)

图 8-7：25LC256 EEPROM 字节写入序列

## 实验 1- 软件

好的，硬件已经讨论过，现在让我们讨论软件。EEPROM 库相当简单，使用 16 位数据作为其参数（2 字节读或 2 字节写）。快速查看下面列出的函数。使用 EEPROM 库函数，我们可以执行 SPI2 的基本初始化以访问 EEPROM，然后在初始化后对其进行读写。

- **InitNVM ()** - 使用 SPI2 初始化 EEPROM 以供访问。在调用任何其他 EEPROM 库函数之前必须先调用此函数。NVM 代表“非易失性存储器”。
- **iReadNVM ( address)**- SPI2 在地址处读取 EEPROM 并返回该位置存储的 16 位值
- **iWriteNVM (address, data)** – SPI2 在指定地址为 EEPROM 写入 16 位数据值。

示例项目 EEPROM.MCW 将用于我们的实验。它使用 PPS 为引脚 18、17、16 配置 SPI2 接口。它为正确操作初始化 SPI2 特殊功能寄存器 SPI2CON1（控制）和 SPI2STAT（状态），最后它将 16 位值写入 EEPROM 中的偶数地址（位于 16 位边界上），然后从 EEPROM 读取该值并比较值。提供了流程图。

![](img/a9229e7b0ddd9608f171b22b52514f39_153_0.png)

// PIC24H 原型 I/O 定义
#define CS EE _RB6 // 串行 EEPROM 选择线
#define TCS EE _TRISB6 // CS EE 引脚的 tris 控制 引脚 11
#define SPI_MASTER 0x0122 // 选择 8 位主模式，CKE=1，SMP=0，4MHz
#define SPI_ENABLE 0x8000 // 使能 SPI 端口，清除状态
void InitNVM(void)
{ // 初始化 SPI 外设
 CS EE = 1; // 选择串行 EEPROM
 TCS EE = 0; // 使 CS EE 引脚为输出
 SPI2CON1 = SPI_MASTER; // 选择模式
 SPI2STAT = SPI_ENABLE; // 使能外设
}
//InitNVM

图 8-11：CS 和 SPI2 初始化

SPI2STAT 和 SPI2CON1 的内容和设置如图 8-11 所示。SPI2CON1 设置为 0x0122，SPI2STAT 设置为 0x8000。这些设置及其含义在图 8-12 和 8-13 中详细说明。

### SPI2STAT SFR 位图

| RW0 | U-0 | RW0 | U-0 | U-0 | U-0 | U-0 | U-0 |
| SPEN | -- | SPISIDL | -- | -- | -- | -- | -- |
| bit 15 |  |  |  |  |  |  | bit 8 |
| U-0 | R/WC-0 | U-0 | U-0 | U-0 | U-0 | R-0 | R-0 |
| -- | SPIROV | -- | -- | -- | -- | SPITBF | SPIRBF |
| bit 7 |  |  |  |  |  |  | bit 0 |
图例：
C = 可清除位   R = 可读位   W = 可写位   U = 未实现位，读为“0”
'-' = 上电复位值   '1' = 位被置位   '0' = 位被清除   'x' = 位未知

SPI2STAT = 0x8000
SPEN =1 使能 SPI

图 8-12：SPI2STAT SFR 设置和位图

### SPI2CON1 SFR 位图

| U-0 | U-0 | U-0 | RW-0 | RW-0 | RW-0 | RW-0 | RW-0 |
| -- | -- | -- | DISSCK | DISSDO | MODE16 | SMP | CKE[1] |
| bit 15 | | | | | | | bit 8 |

| RW-0 | RW-0 | RW-0 | RW-0 | RW-0 | RW-0 | RW-0 | RW-0 |
| SSEN[?] | CKP | MSTEN | SPRE<2:0>[?] | | | PPRE<1:0>[?] | |
| bit 7 | | | | | | | bit 0 |

图例：
R = 可读位    W = 可写位    U = 未实现位，读为“0”
-n = 上电复位值    '1' = 位被置位    '0' = 位被清除    x = 位未知

```
SPI2CON1 = 0x0122
MODE16 = 8 bit mode
SMP =0 (data sample control )
CKE =1 (clock edge)
CKP =0 { clock polarity}
MSTEN =1 (Master Mode Enabled)
SPRE =0 (secondary pre-scale =8:1)
PPRE =2 (primary pre-scale = 4:1)
```

图 8-13：SPI2CON1 SFR 设置和位图

## 实验 1 执行

使用图 8-4 中的原理图构建原型。需要一个 10 k 电阻和一个 25LC256 8 引脚 DIP EEPROM。此外，还需要一个外部 +3.3V DC 电源为 EEPROM 供电（请记住 Microstick II 不提供外部电源）。确保 EEPROM 的地与 Microstick II 的地共用。图 8-14 显示了示例原型装配。将 Microstick II 连接到 PC 的 USB 端口。

![](img/a9229e7b0ddd9608f171b22b52514f39_157_0.png)

图 8-14：组装好的原型

打开第 8 章练习 1 的文件夹并双击 EEPROM.MCW。打开工作区，然后构建并将代码下载到 Microstick II。主代码的快照如下所示。

```
data1 0xAA55; //data values
data2
InitNVM();
iWriteNVM(); data1
data2 ReadNVM 0x1234;

if ( data1 == data0)
Nop(); //break print data compare
else
Nop(); //breakpoint data don't compare

while ... //infinite compare
```

设置数据值

初始化 SPI2 写入到然后从位置 0x1234 读取

比较写入和读取值

无限循环

图 8-14：主线

使用调试器为 data0 和 data1 设置监视。设置所示的两个断点。Nop () 是一个宏，本质上是一个无操作指令。
