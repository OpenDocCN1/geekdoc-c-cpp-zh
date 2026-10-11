
- `1` = 在数据输出时间末尾采样输入数据
- `0` = 在数据输出时间中部采样输入数据

### SPI 从模式
- 当 SPI 用于从模式时，必须清除 `SMP`。

### `CKE` (位 6): SPI 时钟选择位
- `1` = 在时钟状态从活动转换为闲置时发送
- `0` = 在时钟状态从闲置转换为活动时发送
- **注意：** 时钟状态极性由 `CKP` 位（`SSPCON1<4>`）设置。

### `D/A` (位 5): 数据/地址位
- 仅在 I²C™ 模式下使用。

### `P` (位 4): 停止位
- 仅在 I²C 模式下使用。当 MSSP 模块被禁用时，`SSPEN` 被清除，此位被清除。

### `S` (位 3): 起始位
- 仅在 I²C 模式下使用。

### `R/W` (位 2): 读/写信息位
- 仅在 I²C 模式下使用。

### `UA` (位 1): 地址更新位
- 仅在 I²C 模式下使用。

### `BF` (位 0): 缓冲满状态位（仅限接收模式）
- `1` = 接收完成，`SSPBUF` 已满
- `0` = 接收未完成，`SSPBUF` 为空

### 图 11.7 SPI 模式下的 `SSPSTAT` (MSSP Status Register)

![](img/5e76fd429fabd2b62e16a7bfd8cf546f_352_0.png)

**图 11.8** 示例 11.6 中 SPI 模式的示意图

- 3. 使用 `CCPCON1` 寄存器启用串行功能，并选择主模式，时钟频率为 `fosc/4`。
- 4. 将开关输入写入 `WREG`，然后 `CALL` 一个名为 `\_SERIAL\_\_WRITE` 的子程序，将开关数据传输到主机的串行缓冲寄存器（`SSPBUF`）。
- 5. 在循环中等待，检查主机 `SSPSTAT` 寄存器中的 `BF`（Buffer Full，缓冲区满）位是否为 `1`，指示传输完成。
- 6. 一旦 `BF = 1`，程序从子程序返回，并跳转到步骤 4。

#### 从机 PIC18F4321
- 1. 将 `SDI` 和 `SCK` 引脚初始化为输入，将 `PORTD` 初始化为输出。注意 `SCK` 由主机控制，因此从机将其配置为输入。
- 2. 使用从机的 `SSPSTAT` 寄存器选择 `CKE` - 与主机 `CKE` 相同（本例中为高电平到低电平时钟）-。
- 3. 使用从机的 `SSPCON1` 寄存器启用串行功能，禁用 `$\overline{SS}$` 引脚，并选择从机模式。
- 4. 在循环中等待，检查从机 `SSPSTAT` 寄存器中 `BF = 1`。
- 5. 如果 `BF = 0`，则等待。然而，如果 `BF = 1`，将从机的串行缓冲寄存器（`SSPBUF`）的内容输出到从机的 `PORTD`。
- 6. 转到步骤 5。

下面提供了主机和从机微控制器的 PIC18F 汇编语言程序：

```assembly
;Program for the master PIC18F4321
INCLUDE <P18F4321.INC>
    ORG 0x00 ;Reset
    GOTO MAIN
    ORG 0x70
MAIN BCF TRISC, RC5 ;Configure RC5/SD0 as output
BCF TRISC, RC3 ;Configure RC3/SCK as output
MOVLW 0x0F
MOVWF ADCON1 ;Make PORTB digital input
                    MOVLW         5          ; Initialize STKPTR to 5 since subroutine
                    MOVWF         STKPTR     ; called SERIAL_WRITE is used in the
                                              ; program
                    MOVLW         0x40
                    MOVWF         SSPSTAT    ; Set data transmission on high to
                                              ; low clock
                    MOVLW         0x20
                    MOVWF         SSPCON1    ; Enable serial functions and set to
                                              ; master device, and Fosc/4
GET_DATA        MOVF          PORTB,W    ; Move switch value to WREG
                  CALL          SERIAL_WRITE ; Call SERIAL_WRITE function
                  BRA           GET_DATA
SERIAL_WRITE      MOVWF         SSPBUF     ; Move switch value to serial buffer
WAIT               BTSS        SSPSTAT, BF ; Wait until transmission is complete
                  BRA          WAIT
                  RET
                  END
                  ; Program for the slave PIC18F4321
                  INCLUDE <PIC18F4321.INC>
                  ORG           0x00        ; Reset
                  GOTO          MAIN
                  ORG           0x100
MAIN          BSF           TRISC, RC4  ; Configure RC4/SDI as input
                  BSF           TRISC, RC3  ; Configure RC3/SCK as input
                  CLRF          TRISD      ; Configure PORTD as output
                  MOVFW         0x40
                  MOVWF         SSPSTAT    ; Set data transmission on high to
                                              ; low clock
                  MOVFW         0x25
                  MOVWF         SSPCON1    ; Enable serial functions and
                                              ; set to the slave
WAIT          BTSS        SSPSTAT, BF ; Wait until transmission is
                                              ; complete (BF=1)
                  BRA          WAIT       ; If BF=0, wait
                  MOVFF         SSPBUF, PORTD ; Output serial buffer data to
                                              ; PORTD LEDs
                  BRA          WAIT
                  END
```

让我们现在解释上述程序。首先，考虑主机 `PIC18F4321`。`SSPSTAT` 中的 `CKE` 位（位 6）被置为 `1`，以便数据传输发生在从高电平到低电平（HIGH to LOW）的时钟沿。接下来，配置寄存器 `SSPCON1` 以设置串行传输的参数。`SSPCON1` 中的位 `SPEEN`（位 5）被置为高电平，以启用三个引脚，即 `SCK`、`SDO` 和 `SDI`。向 `SSPCON1` 寄存器的 3-0 位写入 `0000` 定义了主模式操作，时钟为 `Fosc/4`。

以下 PIC18F 指令完成了这一设置：

```assembly
MOVFW         0x20 
MOVWF         SSPCON1     ; Enable serial functions and set to master 
                          ; and Fosc/4
```

接下来，考虑从机的 `PIC18F` 汇编语言程序；从机的 `SSPCON1` 的四个位（位 3-0）初始化为 `0101`。这将使微控制器处于从机模式，并且，由于本例中只有一个串行设备，因此 `$\overline{SS}$` 引脚将被禁用。注意，如果使用多个从机设备，则需要 `$\overline{SS}$`。此外，`SCK` 引脚将被用作时钟。

让我们简要解释一下程序逻辑。主机 `PIC18F4321` 的汇编语言程序首先执行所有初始化，输入开关并将其放入 `WREG`。然后程序调用一个名为 `\_SERIAL\_WRITE` 的子程序。该子程序将开关输入移动到 `SSPBUF` 寄存器。一旦主机的串行参数（如 `SCK` 时钟引脚）设置好，数据会自动传输到从机设备。一旦所有数据写入完成，主机微控制器的 `SSPSTAT` 寄存器中的 `BF` 位（位 0）将变为高电平，指示传输完成。

从机微控制器的程序在循环中等待，直到其 `SSPSTAT` 寄存器中的 `BF` 标志变为高电平，表示传输完成。使用 `MOVFF` 指令将从机 `SSPBUF` 寄存器中的开关值输出到连接在 `PORTD` 上的 LED，如下所示：

```assembly
MOVFF         SSPBUF, PORTD ; Move serial buffer value to PORTD.
```

首先，需要使用 `\_PICKit3` 将上述汇编好的程序下载到主机和从机微控制器中。然后，在硬件复位后，主机 `PIC18F4321` 将跳转到地址 `0x70`（任意选择的地址），而从机 `PIC18F4321` 将跳转到地址 `0x100`（任意选择的地址）。注意，两个微控制器不需要同时复位。此外，主机和从机各自独立开始执行各自的程序。主机微控制器执行初始化，连续移动开关数据输入，并在 `GET\_DATA` 循环中等待。从机微控制器也执行初始化，然后在 `WAIT` 循环中等待直到 `BF = 1`。一旦主机和从机之间建立串行通信，主机使用 `SCK` 时钟通过其 `SDO` 引脚将 `SSPBUF` 的内容传输到从机的 `SDI` 引脚。开关数据传输到从机的 `SSPBUF` 寄存器。传输完成后，从机 `SSPSTAT` 寄存器中的 `BF` 位变为 `1`。然后从机通过 `PORTD` 将此数据输出到 LED。

### (b)

可以根据以下步骤为指导编写主机 `PIC18F4321` 和从机 `PIC18F4321` 的 C 语言程序：

#### 主机 PIC18F4321
- 1. 将 `PORTB` 配置为输入，将 `SDO` 和 `SCK` 配置为输出。
- 2. 使用主机的 `SSPSTAT` 寄存器选择 `CKE`（SPI 时钟选择位）。
- 3. 使用 `CCPCON1` 寄存器启用串行功能，并选择主模式，时钟频率如 `FOSC/4`。
- 4. 将开关值放入主机的串行缓冲寄存器（`SSPBUF`）。
- 5. 在循环中等待，检查主机 `SSPSTAT` 寄存器中的 `BF`（Buffer Full，缓冲区满）位是否为 `1`，指示传输完成。
- 6. 一旦 `BF = 1`，程序从子程序返回，并跳转到步骤 4。

#### 从机 PIC18F4321
- 1. 将 `SDI` 和 `SCK` 引脚初始化为输入，将 `PORTD` 初始化为输出。注意 `SCK` 由主机控制，因此从机将其配置为输入。
- 2. 使用从机的 `SSPSTAT` 寄存器选择从机 `CKE`，与主机 `CKE` 相同（本例中为高电平到低电平时钟）。
- 3. 使用从机的 `SSPCON1` 寄存器启用串行功能，禁用 `SS` 引脚，并选择从机模式。
- 4. 在循环中等待，检查从机的 `SSPSTAT` 寄存器中 `BF = 1`。
- 5. 如果 `BF = 0`，则等待。然而，如果 `BF = 1`，将从机的串行缓冲寄存器（`SSPBUF`）的内容输出到从机的 `PORTD`，根据开关打开或关闭 LED。

// 主机 SPI `PIC18F4321` 设备的 C 代码：

```c
#include <p18f4321.h>
void SPI_out(unsigned char);
void main (void)
{
    unsigned char output;
    TRISCbits.TRISC5 = 0;           // Configure SDO as output
    TRISCbits.TRISC3 =0;
    ADCON1=0x0F;                    // Configure PORTB to be digital input
    SSPSTAT= 0x40;                  // Transmission occurs on high to low clock
    SSPCON1 = 0x20;                 // Enable serial functions and set as master device
    while(1){
        output = PORTB;             // Move switch value to output
        SPI_out(output);            // Send variable 'output' to SPI_out
    }
}
void SPI_out(unsigned char SPI_data)
{
    SSPBUF = SPI_data;      // Place switch value into the serial buffer
    while (SSPSTATbits.BF == 0);  // Wait for transmission to finish
}
```

// 从机 `PIC18F4321` 设备的 C 代码：

```c
#include <p18f4321.h>
void main (void)
{
    TRISCbits.TRISC4 = 1;          // Configure SDI as input
    TRISCbits.TRISC3 =1;
    TRISD=0x00;                    // Configure SCK as input
    SSPSTAT= 0x40;                 // Configure PORTD as output for LEDs
    SSPCON1 = 0x25;                // Transmission occurs on high to low clock
    while(1){
    }
}
```

`while (SSPSTATbits.BF == 0);    // 等待传输完成`

`PORTD=SSPBUF;                  // 将串行缓冲区数据移至 PORTD`

### 11.4.2 PIC18F I²C（集成电路总线）模式

如前所述，I²C 协议是由飞利浦（Philips）在 20 世纪 80 年代推出的。这种串行 I/O 最初是为在 PCB（印刷电路板）上连接 IC（集成电路）芯片而开发的。I²C 是同步的，并基于主从（master/slave）操作模式。该协议使用两个引脚：一个用于时钟，一个用于数据。它们是 `SCL`（I²C 模式下的串行时钟引脚，与 Port C 的第 3 位复用）和 `SDA`（I²C 模式下的串行数据引脚，与 Port C 的第 4 位复用）。与 SPI 模式不同，I²C 不需要从机选择（SS）信号。可以使用这两条信号线 `SCL` 和 `SDA` 连接任意数量的主机和从机。这两个信号都是双向的。图 11.9 展示了单个主机与单个从机连接的框图。

I²C 协议规定，在多主/多从系统中，在总线上发起数据传输的主机被视为总线主，所有连接到总机的从设备被视为从机。`SCL` 和 `SDA` 提供开漏输出（需要上拉电阻），以便多个设备可以连接到这些线路上。微芯片（Microchip）建议根据数据传输速率使用以下上拉电阻值：对于低于 100 kbps 的数据速率，使用 4.7 kΩ；对于 100 kbps 的数据速率，使用 2.2 kΩ；对于 400 kbps 的数据速率，使用 1 kΩ。请注意，`bps` 代表每秒位（bits per second）。
