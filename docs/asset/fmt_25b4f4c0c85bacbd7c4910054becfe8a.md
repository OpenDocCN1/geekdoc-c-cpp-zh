
取决于驱动配置，底层数据传输可能由 CPU 执行，也由微控制器提供的内部 DMA 单元执行。

# 查看 Thread.c 中的 CMSIS-Driver 代码

选择项目 `Batch Build` 以编译两个项目。

启动调试器。

在 NXP 项目中，打开 `viewserial\serial 2.`。

打开 `peripherals\USART\usart1` 窗口。

运行代码。

在外设窗口中检查 USART 配置。

初始的 "Hello World" 信息将显示在串口控制台窗口中。

退出调试器。

切换到另一个项目并重复上述操作。

# 477 CMSIS-Driver

一旦初始化了驱动并安装了回调，我们可以通过调用电源控制函数开启外设。

```
USARTdrv->PowerControl(ARM_POWER_FULL);
```

该函数提供了将 USART 置于运行模式所需的底层代码。这通常涉及配置微控制系统控制单元以启用时钟树，并将外设从复位中释放。一旦 USART 通电，我们就可以使用控制函数配置其运行参数。

```
USARTdrv->Control(ARM_USART_MODE_ASYNCHRONOUS |
ARM_USART_DATA_BITS_8 |
ARM_USART_PARITY_NONE |
ARM_USART_STOP_BITS_1 |
ARM_USART_FLOW_CONTROL_NONE, 9600);
```

现在 USART 的运行参数已配置完成，我们可以使用发送和接收函数传输数据。

```
USARTdrv->Send("Message of 26 characters", 26);
USARTdrv->Receive(&cmnd, 1);
```

取决于驱动配置，底层数据传输可能由 CPU 执行，也由微控制器提供的内部 DMA 单元执行。

# 474 第 12 章

- SD/MMC 接口 (`Driver_MCIO`)
- I2C0 (内部集成电路接口 0) [`Driver_I2C0`]
- I2C1 (内部集成电路接口 1) [`Driver_I2C1`]
- USART0 (通用异步收发器...)
- UART1 (通用异步收发器) [`Dr...`]

  - 引脚配置
    - TX
    - RX
    - 调制解调线
  - DMA
    - Tx
    - Rx

图 12.6

在 `RTE_Device.Device.h` 中配置 UART 引脚。

在项目窗口中，打开 `device::RTE_Device.h` 并选择配置向导。

启用 `UART1` 并禁用 DMA 选项。

此示例使用的是仿真器，因此实际引脚配置并不重要。在真实的硬件上，我们需要为 Tx 和 Rx 配置正确的引脚。禁用 DMA 是因为仿真器不支持该外设内的 DMA 单元。

现在打开 `Thread.c`。此文件对于 STM 和 NXP 项目都是通用的。

为了访问 CMSIS-Driver API，我们可以将 USART 驱动头文件添加到我们的源代码中。CMSIS-Driver 为微控制器上提供的每种类型的外设提供支持。每个驱动都由一个访问结构定义，该结构包含了特定外设的 CMSIS-Driver API 定义。

```
ARM_DRIVER_USART_Driver_USART3 = {
USART3_GetVersion,
USART3_GetCapabilities,
USART3_Initialize,
USART3_Uninitialize,
USART3_PowerControl,
USART3_Send,
USART3_Receive,
USART3_Transfer,
USART3_GetTxCount,
USART3_GetRxCount,
USART3_Control,
USART3_GetStatus,
USART3_SetModemControl,
USART3_GetModemStatus
};
```

# CMSIS-Driver 475

要安装驱动支持，我们需要将驱动包含文件添加到我们的源代码中，并为想要访问的 UART 外设添加 "extern" 声明。

```
#include "Driver_USART.h"
extern ARM_DRIVER_USART Driver_USART1;
```

在 `thread.c` 中，我们可以通过第一次 API 调用来初始化驱动。

```
Driver_USART->Initialize(myUSART_callback);
```

初始化调用启动驱动并注册回调函数。在回调函数注册到驱动后，它将由 USART 外设的硬件事件触发，并由驱动中断服务程序调用。每当此函数被触发时，它将接收一个指示特定 USART 硬件事件的参数，如表 12.2 所示。

## 表 12.2：USART 回调事件

| USART 硬件事件 |
| :--- |
| `ARM_USART_EVENT_SEND_COMPLETE` |
| `ARM_USART_EVENT_RECEIVE_COMPLETE` |
| `ARM_USART_EVENT_TRANSFER_COMPLETE` |
| `ARM_USART_EVENT_TX_COMPLETE` |
| `ARM_USART_EVENT_TX_UNDERFLOW` |
| `ARM_USART_EVENT_RX_OVERFLOW` |
| `ARM_USART_EVENT_RX_TIMEOUT` |
| `ARM_USART_EVENT_RX_BREAK` |
| `ARM_USART_EVENT_RX_FRAMING_ERROR` |
| `ARM_USART_EVENT_RX_PARITY_ERROR` |

在回调函数中，我们现在可以为任何想要处理的 USART 硬件事件提供代码。

```
void myUSART_callback(uint32_t event) {
  switch (event) {
    case ARM_USART_EVENT_RECEIVE_COMPLETE:
    case ARM_USART_EVENT_SEND_COMPLETE:
      osSignalSet(tid_Thread, 0x01);
      break;
  }
}
```

现在当 USART 成功发送或接收数据时，回调将被触发，我们可以向其中一个应用程序线程发送 RTOS 事件以指示该事件。

# 476 第 12 章

一旦初始化了驱动并安装了回调，我们可以通过调用电源控制函数开启外设。

```
USARTdrv->PowerControl(ARM_POWER_FULL);
```

该函数提供了将 USART 置于运行模式所需的底层代码。这通常涉及配置微控制系统控制单元以启用时钟树，并将外设从复位中释放。一旦 USART 通电，我们就可以使用控制函数配置其运行参数。

```
USARTdrv->Control(ARM_USART_MODE_ASYNCHRONOUS |
ARM_USART_DATA_BITS_8 |
ARM_USART_PARITY_NONE |
ARM_USART_STOP_BITS_1 |
ARM_USART_FLOW_CONTROL_NONE, 9600);
```

现在 USART 的运行参数已配置完成，我们可以使用发送和接收函数传输数据。

```
USARTdrv->Send("Message of 26 characters", 26);
USARTdrv->Receive(&cmnd, 1);
```

取决于驱动配置，底层数据传输可能由 CPU 执行，也由微控制器提供的内部 DMA 单元执行。
