
# USART 定义了信号传输方法

USART 定义了信号传输方法，但对电压平没有规定说明。这意味着 STM32 USART 将使用 MCU I/O 的电压平，该电压几乎等同 VDD（这些电压平也常被称为 TTL 电平）。为了允许在板外进行串口通信，电压平之间的关系方式需要满足其他通信标准的要求。例如，EIA-RS232 或 EIA-RS485 是两种流行的标准，它们除了定义定时和含义外，定义了信号电压以及连接器的物理尺寸和引脚布局。此外，USART 接口可以用于与其他物理和逻辑接口交换数据。例如，`FT232RL` 是一种常用的 IC，它允许将 UART 转换为 USB 接口，如图 8.4 所示。

专用线路的存在或对传输频率的共同约定，并不能保证字节流的接收器能够以主站相同的传输速率处理数据。由于某些原因，某些通信标准（如 RS232 和 RS485）提供了使用硬件流控线。例如，使用 RS232 接口通信的两个设备可以共享两条额外的线，命名为请求发送 (RTS) 和允许发送 (CTS)：发送端设置其 RTS，信号接收器开始监控其数据输入线。当准备好接收数据时，接收器将升高其互补线 CTS，信号发送端开始发送数据，并且发送端开始监控从机的数据输出线。

# 通用异步串口通信

![](img/9ef247bc7328ae96d937b3818a681558_208_0.png)

图 8.4：基于 FT232RL 的典型电路，用于将 3.3V TTL UART 接口转换为 USB

STM32 微控制器提供了不同数量的 USART，它们可以被配置为在同步和异步模式下工作。某些 STM32 MCU 还提供了仅能作为 UART 使用的接口。表 8.1 列出了本文使用的所有 Nucleo 板所配备的 STM32 MCU 提供的 UART/USART。大多数 USART 能够自动实现硬件流控，同时支持 RS232 和 RS485 标准。

所有 Nucleo-64 板的设计都确保了目标 MCU 的 USART2 连接到 ST-LINK 接口。当我们安装 ST-LINK 驱动程序时，还会安装一个用于虚拟串口端口 (VCP) 的额外驱动程序：这允许我们通过 USB 接口访问目标 MCU 的 USART2，而无需使用专用的 TTL/USB 转换器。使用终端仿真程序，我们可以与我们的 Nucleo 板交换消息和数据。

CubeHAL 提供了管理 UART 和 USART 接口的 API。所有用于管理 USART 的函数和 C 类型处理程序都以 `HAL_UART` 为前缀，并包含在 `stm32xx_hal_uart.{c,h}` 文件中；而与 UART 管理相关的也以 `HAL_UART` 为前缀并包含在 `stm32xx_hal_uart.{c,h}` 文件中。由于两个模块在概念上是相同的，且由于 USART 是不同模块之间串口连接的最常见形式，本书将仅涵盖 `HAL_UART` 模块的功能。

> 请注意，如果你使用的是 Nucleo-32 或 Nucleo-144 板，此说明可能不适用。请检查 ST 文档以获取更多信息。

## 表 8.1：Nucleo 板上的 USART 和 UART

| Nucleo | USART/UART | USART | RS232 流控 | RS485 流控 |
|---|---|---|---|---|
| Nucleo-F446 | 4 + 2 | 6 | Y | Y |
| Nucleo-G474 | 3 + 2 | 5 | Y | Y |
| Nucleo-F401 | 4 + 2 | 6 | Y | Y |
| Nucleo-F303 | 3 + 2 | 5 | Y | Y |
| Nucleo-F072 | 2 + 1 | 3 | Y | Y |
| Nucleo-F206 | 3 + 1 | 4 | Y | Y |
| Nucleo-L476 | 3 + 2 | 5 | Y | Y |
| Nucleo-L152 | 3 + 2 | 5 | Y | - |

## 8.2 UART 初始化

像 STM32 微控制器一样，USART 映射到 `USART_TypeDef`。例如，USART2 是与 ST-LINK 接口关联的描述器。相关的 USART 函数如下所示定义：

> 请注意，除非特别说明，否则 USART 和 UART 名称是通用的。

> 此结构体的分析不在本书范围之内。

> 如需更多信息，请参考 CubeHAL。

```c
typedef struct {
    USART_TypeDef *Instance;                                  /* UART 寄存器基址  */
    UART_InitTypeDef Init;                                    /* UART 通信参数 */
    UART_AdvFeatureInitTypeDef AdvancedInit;                  /* 高级功能初始化参数 */
    uint8_t *pTxBuffPtr;                                      /* 指向发送缓冲区 */
    uint16_t TxXferSize;                                      /* UART 传输大小 */
    uint16_t TxXferCount;                                     /* 传输计数 */
    uint8_t *pRxBuffPtr;                                      /* 指向接收缓冲区 */
    uint16_t RxXferSize;                                      /* UART 接收大小 */
    uint16_t RxXferCount;                                     /* 接收计数 */
    DMA_HandleTypeDef hdmatx;                                 /* UART DMA 句柄 */
    DMA_HandleTypeDef hdmarx;                                 /* 接收 DMA 句柄 */
    HAL_LockTypeDef Lock;                                     /* 锁对象               */
    __IO HAL_UART_StateTypeDef gState;                        /* UART 通信状态      */
    __IO HAL_UART_ErrorTypeDef ErrorCode;                     /* UART 错误代码               */
} UART_HandleTypeDef;
```

让我们深入查看该结构体最重要的字段。

- `Instance`：指向描述器的指针（即外设映射的内存基地址）。例如，USART2 是与每个 Nucleo 板的 ST-LINK 接口关联的描述器。
- `Init`：`UART_InitTypeDef` 结构体的实例，用于配置 UART 接口。我们将在后续中深入研究它。
- `AdvancedInit`：此字段用于配置更高级的 UART 功能，如波特率检测和 TX/RX 切换。某些 HAL 未提供此额外字段，因为 STM32 MCU 的 UART 接口并不相同。在选择合适的 MCU 时，这是一个需要考虑的重要方面。该字段的分析不在本文范围内。
- `pTxBuffPtr`、`pRxBuffPtr`：这些字段分别指向发送和接收缓冲区。当 UART 配置为全双工模式时，它们作为传输接收字节的源。`TxXferCount` 和 `RxXferCount` 字段由 HAL 内部使用，记录传输和接收字节的计数。
- `Lock`：此字段由 HAL 内部使用，用于锁定 UART 接口的并发访问。

如上所述，`Lock` 字段用于控制几乎所有的 HAL 例程中的并发访问。如果你查看 HAL 代码，你会看到多处对 `__HAL_LOCK()` 宏的使用，它的展开方式如下：

```c
#define __HAL_LOCK(__HANDLE__) \
do { \
    if((__HANDLE__)->Lock == HAL_LOCKED) { \
        return HAL_BUSY; \
    } \
    else { \
        (__HANDLE__)->Lock = HAL_LOCKED; \
    } \
} while (0)
```

目前还不清楚 ST 工程师为何决定处理 HAL 例程的并发访问。可能他们是决定在同一个应用程序中运行多个线程的情况下，承担管理对同一硬件接口的多次访问的责任。

然而，这对于所有 HAL 用户来说带来了一个恼人的副作用：即使我的应用程序没有对同一个外设进行并发访问，我的代码也会因为大量关于 `Lock` 字段状态的检查而导致优化不良。此外，当更高级别的中断服务程序（ISR）抢占正在运行的代码时，并没有使用临界区来防止竞争条件。最后，如果我的应用程序使用了 RTOS，那么使用原生操作系统锁原语（如信号量和互斥量）要好得多，因为这些不仅是原子的，还能正确地管理任务调度，避免为了处理并发访问而进行忙等，且无需检查 HAL 函数的特定返回值（`HAL_BUSY`）。

自 HAL 首次发布以来，许多开发者一直反对这种锁定外设的方法。ST 工程师在几年前宣布过他们正在积极开发一种更好的解决方案。然而，目前还没有相关消息。

所有的 UART 配置活动都是通过使用 `UART_InitTypeDef` 结构体实例完成的，其定义方式如下：

```c
typedef struct {
    uint32_t BaudRate;
    uint32_t WordLength;
    uint32_t StopBits;
    uint32_t Parity;
    uint32_t Mode;
    uint32_t HwFlowCtl;
    uint32_t OverSampling;
} UART_InitTypeDef;
```

- **波特率**：此参数指的是连接速度，以每秒位数（bits）表示。尽管该参数可以接受任意值，但通常 `BaudRate` 来自一组已知且标准的值的列表。因为它是与 USART 关联的外设时钟的函数（该时钟在某些 STM32 MCU 中通过 PLL 和倍频器从主 HSI 或 HSE 时钟衍生），而且在不引入采样错误的情况下无法实现所有的 BaudRates。表 8.2 显示了 STM32F072 MCU 的常见波特率列表以及相关的误差计算。请始终查阅您的 MCU 的参考手册，以查看哪个外设时钟频率最适合您 STM32 微控制器上的 BaudRate。

### 表 8.2：在 48 MHz 下，16 倍或 8 倍过采样两种情况下设置波特率的误差计算

| 序号 | 目标 (Bps) | 16倍过采样实际 | 16倍过采样误差 % | 8倍过采样实际 | 8倍过采样误差 % |
|---|---|---|---|---|---|
| 2 | 2400 | 2400 | 0 | 2400 | 0 |
| 3 | 9600 | 9600 | 0 | 9600 | 0 |
| 4 | 19200 | 19200 | 0 | 19200 | 0 |
| 5 | 38400 | 38400 | 0 | 38400 | 0 |
| 6 | 57600 | 57620 | 0.03 | 57590 | 0.02 |
| 7 | 115200 | 115110 | 0.08 | 115250 | 0.04 |
| 8 | 230400 | 230760 | 0.16 | 230210 | 0.8 |
| 9 | 460800 | 461540 | 0.16 | 461540 | 0.16 |
| 10 | 921600 | 923070 | 0.16 | 923070 | 0.16 |
| 11 | 2000000 | 2000000 | 0 | 2000000 | 0 |
| 12 | 3000000 | 3000000 | 0 | 3000000 | 0 |
| 13 | 4000000 | N.A. | N.A. | 4000000 | 0 |
| 14 | 5000000 | N.A. | N.A. | 5052630 | 1.05 |
| 15 | 6000000 | N.A. | N.A. | 6000000 | 0 |

- **数据长度**：此参数指的是数据帧中的位数。
- **停止位**：此参数定义了帧结束使用的停止位数量。
- **校验位**：此参数决定了使用的奇偶校验方法。
- **模式**：此参数设置了工作模式（RX、TX 或两者）。
- **硬件流控**：此参数启用或禁用硬件流控（RTS/CTS）。
- **过采样**：此参数定义了数据恢复的过采样率。

现在是写一些代码的好时机。让我们看看如何配置 Nucleo 的 USART2 通过 ST-LINK 接口交换消息。

```c
int main(void) {
  UART_HandleTypeDef huart2;

  /* 初始化 HAL */
  HAL_Init();

  /* 配置系统时钟 */
  SystemClock_Config();

  /* 配置 USART2 */
  huart2.Instance = USART2;
  huart2.Init.BaudRate = 34800;
  huart2.Init.WordLength = UART_WORDLENGTH_8B;
  huart2.Init.StopBits = UART_STOPBITS_1;
  huart2.Init.Parity = UART_PARITY_NONE;
  huart2.Init.Mode = UART_MODE_TX_RX;
  huart2.Init.HwFlowCtl = UART_HWCONTROL_NONE;
  huart2.Init.Oversampling = UART_OVERSAMPLING_16;
  HAL_UART_Init(&huart2);

  while (1) {
  }
}
```

第一步是配置 USART2 外设。在这里我们使用以下配置：34800, N。即波特率等于 34800 Bps，无奇偶校验且仅有一个停止位。接下来，我们禁用硬件流控的形式，我们选择了最高的过采样率，即每个传输位对应 16 个时钟脉冲。调用 `HAL_UART_Init()` 函数确保了 HAL 根据给定的选项初始化 USART2。

然而，上述代码仍然不足以通过 Nucleo 串口交换消息。不要忘记，每个与外部世界交换数据的外设设备都必须通过配置 GPIO 进行正确绑定，因此我们必须配置 USART2 的 TX 和 RX 引脚。查看 Nucleo 的原理图，我们可以看到 USART2 的 TX 和 RX 引脚分别为 PA2 和 PA3。此外，我们已经在第 4 节中看到，HAL 的设计使得 `HAL_UART_Init()` 函数会自动调用 `HAL_UART_MspInit()` 函数（见第 4 节图 4.15）来正确初始化 I/O；我们的职责是在应用程序代码中编写此函数，该函数将由 HAL 调用。

### 必须定义此函数吗？

答案很简单。这只是 HAL 强制的一种做法，也是 CubeMX 自动生成的代码。`HAL_UART_MspInit()` 以及由 `HAL_UART_DeInit()` 函数调用的相应函数 `HAL_UART_MspDeInit()` 以如下方式包含：

```c
__weak void HAL_UART_MspInit(UART_HandleTypeDef* huart);
```

函数属性 `__weak` 是 GCC 的语法，用于声明一个具有弱作用范围的符号（此处为函数名），如果在应用程序的别处（即另一个可重定位文件）定义了具有全局作用范围的符号（即不带 `__weak` 属性），则该符号将被覆盖。如果我们在应用程序代码中实现了函数 `HAL_UART_MspInit()`，链接器将自动替换对 HAL 内部定义的 `HAL_UART_MspInit()` 函数的调用。

以下代码展示了如何正确编写 `HAL_UART_MspInit()` 函数：

```c
void HAL_UART_MspInit(UART_HandleTypeDef* huart) {
  GPIO_InitTypeDef GPIO_InitStruct;
  if(huart->Instance == USART2) {
    /* 外设时钟开启 */
    HAL_RCC_USART2_CLK_ENABLE();

    /* USART2 GPIO 配置
    PA2       ------ USART2_TX
    PA3       ------ USART2_RX
    */
    GPIO_InitStruct.Pin = GPIO_PIN_2 | GPIO_PIN_3;
    GPIO_InitStruct.Mode = GPIO_MODE_AF_PP;
    GPIO_InitStruct.Pull = GPIO_NOPULL;
    GPIO_InitStruct.Speed = GPIO_SPEED_LOW;
    GPIO_InitStruct.Alternate = GPIO_AF1_USART2; /* 警告：这取决于特定的 STM32 MCU */

    HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);
  }
}
```

如你所见，该函数的设计适用于应用程序内部使用的每个 USART。如果该语句规定了给定 USART（在我们的例中为 USART2）的初始化代码，其余代码配置了 PA2 和 PA3 引脚。**请注意，复用功能可能会根据配备 Nucleo 板的 MCU 而变化。** 请参考书籍示例查看适用于你的 Nucleo 的正确初始化代码。
