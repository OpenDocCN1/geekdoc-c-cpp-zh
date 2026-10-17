
```c
while (HAL_I2C_GetState(&hi2c1) != HAL_I2C_STATE_READY);

printf(uartBuf, "WHO AM I: %x\r\n", i2cBuf[0]);

HAL_UART_Transmit(&huart2, (uint8_t*)uartBuf, strlen(uartBuf), HAL_MAX_DELAY);

i2cBuf[0] = TEMP_OUT_IN_REGISTER;

HAL_I2C_Master_Sequential_Transmit(&hi2c1, I2C_SLAVE_ADDR, i2cBuf,
                               1, I2C_FIRST_FRAME);

while (HAL_I2C_GetState(&hi2c1) != HAL_I2C_STATE_READY);

HAL_I2C_Master_Sequential_Receive(&hi2c1, I2C_SLAVE_ADDR, (uint8_t*)&int,
                               1, I2C_LAST_FRAME);

while (HAL_I2C_GetState(&hi2c1) != HAL_I2C_STATE_READY);

i2cBuf[0] = TEMP_OUT_FRAC_REGISTER;

HAL_I2C_Master_Sequential_Transmit(&hi2c1, I2C_SLAVE_ADDR, i2cBuf,
                               1, I2C_FIRST_FRAME);

while (HAL_I2C_GetState(&hi2c1) != HAL_I2C_STATE_READY);

#endif
```

SPI 总线由四个信号组成，如图 15.1 所示，即使可以使用三个 I/O 驱动某些 SPI 设备（在这种情况下我们讨论的是 3 线 SPI）：

- `SCK`：此信号 I/O 用于产生时钟，以同步 SPI 总线上的数据传输。它由主设备产生，这意味着 SPI 总线传输始终由主设备启动。与 IC 规范不同，SPI 本质上更快，且 SPI 时钟通常为几 MHz。现在，能够以高达 100MHz 的速率交换数据的 SPI 设备已经非常常见。此外，SPI 协议允许不同通信速度的设备在同一条总线上共存。
- `MOSI`：该信号 I/O 的名称代表主输出输入（Master Output Input），用于从主设备发送数据到从设备。与 IC 总线使用一根线进行双向数据交换不同，SPI 协议定义了两条不同的线来在主设备和从设备之间交换数据。
- `Sn`：它代表从机选择（Slave Select），在典型的 SPI 总线中，存在“n”条独立的信号线来寻位参与事务的特定 SPI 设备。与 IC 协议不同，SPI 不使用从机地址来选择设备，而是要求对物理线进行拉低电平（LOW）以执行选择。在典型的 SPI 总线上，通过拉低其 SS 线，同时只有一个从设备处于激活状态。这就是为什么不同通信速度的设备可以在同一条总线上共存的原因。

由于具有两条独立的数据通信线 `MOSI` 和 `MISO`，SPI 本质上允许全双工通信，因为从设备在从主设备接收新数据的同时，可以向主设备发送数据。在点对点 SPI 总线（只有一个主设备和一个从设备）中，可以省略 `SS` 信号（相应的从机 I/O 接地），并将 `MISO`/`MOSI` 线合并为单线从机输入/从机输出（`SISO`）。在这种情况下我们称为 2 线 SPI，即使它本质上是一个 3 线总线。

> 为了起见，我们必须说明，这并不是在同一总线上可以拥有不同通信速度设备的准确原因。主要原因在于从机 I/O 是用三态 I/O 实现的，当 `SS` 线未被拉低电平时，它们会处于高阻态状态（断开连接）。

![](img/9ef247bc7328ae96d937b3818a681558_445_0.png)

图 15.2：全双工传输中 SPI 总线上的数据交换方式

总线上的每次事务都是根据最大从机频率启用 `SCK` 线开始的。一旦时钟线开始产生信号，`SS` 线拉低，数据传输即可开始。事务通常涉及两个给定字宽的寄存器，一个在主设备中，一个在从设备中。数据通常从最高位（`MSB`）开始移出，同时向寄存器中移入一个新的最低位（`LSB`）。与此同时，来自从设备的数据移入最低位寄存器。如果需要交换更多数据，则重新加载移位寄存器并重复该过程。传输可以持续任意数量的时钟周期。完成后，主设备停止切换时钟信号，并通常取消选择从设备。

图 15.2 显示了全双工传输中的数据传输方式，而图 15.3 显示了在半双工连接中通常的交换方式。

![](img/9ef247bc7328ae96d937b3818a681558_445_1.png)

图 15.3：半双工传输中 SPI 总线上的数据交换方式

> 8 位数据传输是常规，但某些从设备支持 16 位传输。

## 15.1.1 时钟极性和相位

除了设置总线频率外，主设备和从设备还必须就通过 `MOSI` 和 `MISO` 线交换的数据的时钟极性和相位一致。摩托罗拉的 SPI 规范将这两个设置命名为 `CPOL` 和 `CPHA`，大多数芯片供应商都采用了这一惯例。

极性和相位的组合通常称为 SPI 总线模式，编号如表 15.1 所示。最常见的模式是模式 0 和模式 3，但大多数从设备至少支持两种总线模式。

表 15.1：根据 `CPOL` 和 `CPHA` 的 SPI 总线模式

| 模式 | CPOL | CPHA |
|---|---|---|
| 0 | 0 | 0 |
| 1 | 0 | 1 |
| 2 | 1 | 0 |
| 3 | 1 | 1 |

时序如图 15.4 所示，并在下方进一步描述：

- 在 `CPOL=0` 时，时钟的基础值为 0，即有效状态为 1，空闲状态为 0。
- `CPHA=0` 时，数据在 `SCK` 上升沿（LOW → HIGH 跳）采样，数据在下降沿（HIGH → LOW）输出。
- `CPHA=1` 时，数据在 `SCK` 下降沿采样，数据在上升沿输出。
- 在 `CPOL=1` 时，时钟的基础值为 1（`CPOL=0` 的反反），即有效状态为 0，空闲状态为 1。
- `CPHA=0` 时，数据在 `SCK` 下降沿采样，数据在上升沿输出。
- `CPHA=1` 时，数据在 `SCK` 上升沿采样，数据在下降沿输出。
因此，`CPHA=0` 意味着在第一个时钟沿采样，而 `CPHA=1` 意味着在第二个时钟沿采样，无论该沿是上升还是下降。注意，当 `CPHA=0` 时，数据必须保持稳定。

![](img/9ef247bc7328ae96d937b3818a681558_445_0)

图 15.4：根据 `CPOL` 和 `CPHA` 的 SPI 时序图

## 15.1.2 从机选择

如所述，从设备在总线上并不通过地址选择，而是通过将 `SS`（从机选择）信号拉低来执行选择。STM32 微控制器提供了多种模式来处理 `SS` 信号：

- 软件模式：`SS` 由任何 GPIO 驱动。当主设备工作时，固件可以拉低该引脚来选择它。
- 硬件模式：`SS` 由特定的 I/O 驱动，由外设内部管理。
- 输出模式：此配置用于主设备，`SS` 引脚作为输出使用。当主设备工作时，`SS` 信号被拉低。
- 禁用模式：此配置允许多个设备共存，`SS` 信号被禁用。

## 15.1.3 TI 模式

STM32 微控制器在作为主设备工作时支持 TI 模式。在 TI 模式下，时钟极性和相位遵循德州仪器（TI）的要求。在 TI 模式下，`SS` 信号在每个字节的结束处产生脉冲（从 LOW 变为 HIGH），在 `LSB` 位开始时从 HIGH 变为 LOW。关于此模式的更多信息，请参考参考手册。

| Nucleo P/N | MOSI | SCK | MOSI | SCK | PA10 | PF1 | PC12 | MISO | PC10 |
|---|---|---|---|---|---|---|---|---|---|
| NUCLEO-G47RE | PA7 | PA6 | PA5 | PA11 | | | PC11 | PC10 |
| | PB5 | PB4 | PB3 | PB15 | PB14 | PB13 | PB4 | PB3 |
| NUCLEO-F44RE | PA7 | PA6 | PA5 | PC1 | PC2 | PB10 | | PC10 |
| | PB5 | PB4 | PB3 | PB15 | PB14 | PB13 | PB2 | PB4 |
| NUCLEO-F401RE | PA7 | PA6 | PA5 | PC3 | | | PC12 | PC10 |
| | PB5 | PB4 | PB3 | PB15 | PB14 | PB13 | PB5 | PB4 | PA3 |
| NUCLEO-F303RE | PA7 | PA6 | PA5 | PB15 | PB14 | PB13 | PC12 | PC10 | |
| | PB5 | PB4 | PB3 | PA11 | PA10 | PF1 | PB5 | PB4 | PB3 |
| NUCLEO-F103RE | PA7 | PA6 | PA5 | PB13 | | | | | | |
| | PB5 | PB4 | PB3 | | | | | | | |
| NUCLEO-F072RE | PA7 | PA6 | PB3 | PC3 | PC2 | PB10 | | | | |
| | PB5 | PB4 | PA5 | PB15 | PB14 | PB13 | | | | |
| NUCLEO-L476RG | PA7 | PA6 | PA5 | PC3 | PC2 | PB10 | PC12 | PC11 | PC10 |
| | PB5 | PB4 | PB3 | PB15 | PB14 | PB13 | PB5 | PB4 | PA3 |
| NUCLEO-L152RE | PA7 | PA6 | PB3 | PB15 | PB14 | PB13 | PC12 | PC11 | PC10 |
| | PB5 | PB4 | PB5 | | | | PB5 | PB4 | PB3 |
| NUCLEO-L073RZ | PA7 | PA6 | PA5 | PC3 | PC2 | PB10 | | | | |
| | PB5 | PB4 | PB3 | | | | | | | |

## 12.2 HAL_SPI 模块

为了编程 SPI 外设，HAL 定义了 C 结构体 `SPI_HandleTypeDef`，定义如下：

```c
typedef struct __SPI_HandleTypeDef {

    /* SPI 寄存器基地址 */

    SPI_TypeDef             *Instance;      /* SPI 通信参数 */

    SPI_InitTypeDef        Init;           /* 指向 SPI 传输缓冲区指针 */

    uint8_t                 *pTxBuffPtr;     /* SPI 传输大小 */

    uint16_t                TxFerSize;      /* SPI 传输计数器 */

    __IO uint16_t           TxFerCount;     /* SPI 传输计数器 */

    uint8_t                 *pRxBuffPtr;     /* 指向 SPI 接收缓冲区指针 */

    uint16_t                RxFerSize;      /* SPI 接收传输大小 */

    __IO uint16_t           RxFerCount;     /* SPI 接收计数器 */

    DMA_HandleTypeDef      *hdmadx;        /* SPI DMA 句柄参数 */

    DMA_HandleTypeDef      *hdmarx;        /* SPI DMA 句柄参数 */

    HAL_LockTypeDef         Lock;           /* 锁对象 */

    __IO HAL_SPI_StateTypeDef *State;      /* SPI 通信状态 */

    __IO int32_t            ErrorCode;      /* SPI 错误代码 */

} SPI_HandleTypeDef;
```

让我们分析此结构体中最重要的字段：

- `Instance`：指向我们将使用的 SPI 描述符的指针。例如，`SPI1` 是第一个 SPI 外设的描述符。
- `Init`：C 结构体 `SPI_InitTypeDef` 的实例，用于配置外设。它将在内存中保留一段时间。
- `pTxBuffPtr`, `pRxBuffPtr`：指向用于临时存储传输到 SPI 外设数据的内部缓冲区指针。这用于 SPI 处于中断模式时，且不应由用户代码修改。
- `hmadx`, `hdmarx`：当 SPI 外设在 DMA 模式下运行时 `DMA_HandleTypeDef` 结构体实例指针。

SPI 外设的设置通过 C 结构体 `SPI_InitTypeDef` 的实例完成，其定义如下：

```c
typedef struct {

    uint32_t Mode;           /* 指定 SPI 运行模式。 */

    uint32_t Direction;      /* 指定 SPI 双向模式状态。 */

    uint32_t DataSize;       /* 指定 SPI 数据大小。 */

    uint32_t CKPolarity;     /* 指定串行时钟稳态。 */

    uint32_t CKPhase;        /* 指定用于位捕的时钟有效边沿。 */

    uint32_t NSS;            /* 指定 NSS 信号由硬件（NSS 引脚）还是软件管理 */

    uint32_t BaudRatePrescaler;/* 指定配置 K 时钟的波特分频值。 */

    uint32_t FirstBit;       /* 指定数据传输从 MSB 还是 LSB 位开始。 */

    uint32_t TIMode;         /* 指定是否启用 TI 模式。 */

    uint32_t CRCCalculation;  /* 指定是否启用 CRC 计算。 */

    uint32_t CRCPolynomial;  /* 指定用于 CRC 计算的多项式。 */

} SPI_InitTypeDef;
```

- `Mode`：将 SPI 设置为主机模式或从机模式。它可以取值 `SPI_MODE_MASTER` 和 `SPI_MODE_SLAVE`。
- `Direction`：配置外设以 4 线（输入/输出分开的两根线）或 3 线（一根 I/O 线）运行。它可以取值 `SPI_DIRECTION_2_LINES` 来配置全双工 4 线模式；取值 `SPI_DIRECTION_1_LINES_RXONLY` 来配置半双工 3 线模式。
- `DataSize`：配置 SPI 总线上的数据大小，它可以取值 `SPI_DATASIZE_8BIT` 和 `SPI_DATASIZE_16BIT`。
- `CKPolarity`：配置 `SCK` `CPOL` 设置，它可以取值 `SPI_POLARITY_LOW`（对应 `POL=0`）和 `SPI_POLARITY_HIGH`（对应 `POL=1`）。
- `CKPhase`：这与设置的时钟相位有关，它可以取值 `SPI_PHASE_EDGE`（对应 `CPHA=0`）和 `SPI_PHASE_2_EDGE`（对应 `CPHA=1`）。
- `NSS`：该字段定义 `NSS` I/O 的行为。可以取值 `SPI_NSS_SOFT` 配置为软件模式；取值 `SPI_NSS_HARD_INPUT` 和 `NSS_HARD_OUTPUT` 分别配置硬件输入和输出的 `NSS` 信号。
- `BaudRatePrescaler`：设置 `K` 时钟的分频器并建立最大 `SCK` 时钟速度。它可以取值 `SPI_BAUDRATEPRECALER_2`、`SPI_BAUDRATEPRECALER_4` 直到 `SPI_BAUDRATEPRECALER_256`（从 2 到 27 的所有幂）。
- `FirstBit`：设置传输方向，它可以取值 `SPI_FIRSTBIT_MSB` 和 `SPI_FIRSTBIT_LSB`。
- `TIMode`：用于启用/禁用 TI 模式，它可以取值 `SPI_TIMODE_DISABLE` 和 `SPI_TIMODE_ENABLE`。
- `CRCCalculation` 和 `CRCPolynomial`：所有 STM32 微控制器中的 SPI 都支持硬件 CRC 生成。CRC 值可以在 Tx 模式下作为最后一个字节传输，或者对最后一次接收进行自动 CRC 错误检查。CRC 值使用一个旧的可编程多项式对每个位进行计算。计算由 `CPHA` 和 `CPOL` 配置定义的采样时钟边沿处理。计算出的 CRC 值会在数据块结束以及由 CPU 或 DMA 管理的传输时自动检查。当检测到接收数据内部计算的 CRC 与发送端的 CRC 不匹配时，将设置错误状态。当 SPI 处于 DMA 循环模式时，CRC 功能不激活。关于此选项的更多信息，请参考你所考虑的 STM32 MCU 的参考手册。

与通常，配置 SPI 外设我们使用函数：

```c
HAL_StatusTypeDef HAL_SPI_Init(SPI_HandleTypeDef *hspi);
```
