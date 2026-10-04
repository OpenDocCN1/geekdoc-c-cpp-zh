
## 8.4 中断模式下的 UART 通信

再次考虑本章的示例。它有什么问题？由于我们的固件致力于完成这个简单任务，使用轮询模式 UART 没有问题。MCU 本质上在等待用户输入（`HAL_MAX_DELAY` 超时值会阻塞 `HAL_UART_Receive()` 直到字符发送到 UART）。但如果我们的固件需要实时执行 CPU 密集型活动呢？

假设重排第一个示例中的 `main()` 函数：

```c
while (!) {
    opt = readUserInput();
    processUserInput(opt);
    if (opt == 3)
        goto sendMessage;
}

performCriticalTasks();
```

在这种情况下，我们无法阻塞 `processUserInput()` 的执行来等待用户，但必须为 `HAL_UART_Receive()` 函数使用某些超时值，否则 `performCriticalTasks()` 永远不会执行。然而，这可能会导致来自 UART 的重要数据丢失（记住 UART 接口只有一个字节缓冲区）。

为了解决这个问题，提供了另一种通过 UART 外设交换数据的方法：中断模式。使用此模式，我们必须执行以下操作：

- 启用 `USART_x_IRQ` 中断并实现相应的 `USART_x_IRQHandler()`。
- 在 `USART_x_IRQHandler()` 内部调用 `HAL_UART_IRQHandler()`：这将执行与 UART 外设产生的中断管理的所有活动。
- 使用函数 `HAL_UART_Transmit_IT()` 和 `HAL_UART_Receive_IT()` 通过 UART 交换数据。这些函数也开启 UART 外设的中断模式：通过这种方式，当事件发生时触发 ISR。
- 设计我们的应用程序代码来处理异步事件。

在重排第一个示例的代码之前，查看可用 UART 中断以及 HAL 例程的设计方式最好。

### 8.4.1 UART 相关中断

每个 STM32 UART 外设都提供表 8.6 列出的中断。这些中断包含了与数据传输和通信错误相关的中断。它们可以分为两组：

- 传输期间产生的中断：传输完成、发送准备或传输数据寄存器空。
- 接收期间产生的中断：空闲链路检测、溢出错误、接收数据寄存器非空、校验错误、噪声标志（仅限多缓冲区通信）和帧错误（仅多缓冲区通信）。

> 如果我们使用 CubeMX 启用 NVIC 中的 `USART_x_IRQ` 配置部分（如第 7 章所示），它会自动在 ISR 中放置对 `HAL_UART_IRQHandler()` 的调用。

## 表 8.6：USART 输出列表

| 中断事件 | 事件标志 | 允许控制位 |
| :--- | :--- | :--- |
| 传输数据寄存器空 | TXE | TXEIE |
| 发送完成 (CTS) 标志 | CTS | CTSIE |
| 传输完成 | TC | TCIE |
| 接收数据准备就读 | RXNE | RXNEIE |
| 检测到溢出错误 | ORE | RXNEIE |
| 检测到空闲链路 | IDLE | IDLEIE |
| 校验错误 | PE | PEIE |
| 空断标志 | LBD | LBDIE |
| 多缓冲区通信中的噪声标志、溢出错误和帧错误 | NF 或 OR 或 FE | EIE |

如果设置了相应的允许控制位（表 8.6 第三列），这些事件就会产生中断。然而，STM32 MCU 的设计使得每个 USART 外设的这些中断都绑定到一个 ISR（见图 8.10）。

![](img/9ef247bc7328ae6d937b381a681558_0.png)
图 8.10: USART 中断事件连接到同一个中断向量

从技术角度来看，轮询模式和中断模式下的 UART 传输并没有太大区别。两种方法都使用 UART 寄存器 (DR) 传输字节数组，算法如下：

CubeHAL 设计用于自动为你完成这项工作。通过一组由 `HAL_UART_IRQHandler()` 调用的回调函数来告知用户中断生成，该函数必须如前所述在 ISR 中调用。

> ¹图 8.10 取自 STM32F030 参考手册 (RM0390)。

### 通用异步串口通信

- 对于传输，将一个字节放置在 `USART->DR` 寄存器中，并等待发送数据寄存器空（TXE）标志位被置为真（true）。
- 对于接收，等待接收数据准备就绪读取（RXNE）不被置为真，然后将 `USART->DR` 寄存器的内容存储在应用程序内存中。

这两种方法的区别在于它们如何等待数据传输的完成。在轮询模式下，`HAL_UART_Receive()`/`HAL_UART_Transmit()` 函数的设计是：无论我们想要传输什么，它都会等待相应的事件标志位被设置。在中断模式下，`HAL_UART_Receive_IT()`/`HAL_UART_Transmit_IT()` 函数的设计是它们不等待数据传输完成，而是将新字节放入 DR 寄存器中或将其内容加载到应用程序内存中的“脏活”，是在生成了 RXNEIE/TXIE 中断时由 ISR 例行程序完成的。

要在中断模式下传输字节序列，HAL 定义了以下函数：

```c
HAL_TypeDef HAL_UART_Transmit_IT(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size);
```

其中：

- `huart`: 指向之前 `UART_HandleTypeDef` 结构体实例的指针，该实例用于识别和配置 UART 外设；
- `pData`: 指向数组的指针，其长度与 `Size` 参数相等，包含了我们要传输的字节序列；该函数不会阻塞等待数据传输，一旦完成 UART 的配置，它就会将控制权交还给主流程。

相反，要在中断模式下通过 USART 接收字节序列，HAL 提供了以下函数：

```c
HAL_TypeDef HAL_UART_Receive_IT(UART_HandleTypeDef *huart, uint8_t *pData, uint16_t Size);
```

其中：

- `huart`: 指向之前过的 `UART_HandleTypeDef` 结构体实例的指针，该实例用于识别和配置 UART 外设；
- `pData`: 指向数组的指针，其长度至少等于 `Size` 参数，包含了我们要接收的字节序列。该函数不会阻塞等待数据接收，一旦完成 UART 的配置，它就会将控制权交还给主流程。

现在我们可以继续重新排列第一个示例了。

> 这就是为什么当通信速度过高或我们每隔一段时间就要传输大量数据时，在中断模式下传输字节序列不是一件明智的事。由于每个字节的传输发生得很快，CPU 会被 UART 为每个字节产生的中断所“淹没”。对于高速连续传输大量字节序列，最好是使用 DMA 模式，我们将在下一节看到。

### 通用异步串口通信

文件名：`src/main-ex2.c`

```c
/*  USART USART2中断 */
HAL_NVIC_SetPriority(USART2_IRQn, 0, 0);
HAL_NVIC_EnableIRQ(USART2_IRQn);

printMessage();

printWelcomeMessage();

while (1) {
    opt = readUserInput();
    if(opt > 0) {
        processUserInput(opt);
        if(opt == 3) {
            goto printMessage();
        }
    }
    performCriticalTasks();
}

void USART2_IRQHandler(void) {
    HAL_UART_IRQHandler(&huart2);
}

void HAL_UART_RxCompleteCallback(UART_HandleTypeDef *UartHandle) {
    /* 设置传输标志：传输完成*/
    UartReady = SET;
}

void printWelcomeMessage(void) {
    char *strings[] = {"\033[0H", "\033[2J", WELCOME_MSG, MAIN_MENU, PROMPT};
    for (uint8_t i = 0; i < 5; i++) {
        HAL_UART_Transmit_IT(huart2, (uint8_t*)strings[i], strlen(strings[i]));
        while (HAL_UART_GetState(&huart2) == HAL_UART_STATE_BUSY);
    }
}

int8_t readUserInput(void) {
    int8_t retval = -1;

    if(UartReady == SET) {
        UartReady = RESET;
        HAL_UART_Receive_IT(&huart2, readBuf, 1);
        retval = atoi(readBuf);
    }
    return retval;
}
```

### 通用异步串口通信

101 返回值

102 通用

2（见上方代码 83:91）。在这种实现中，我们在使用 `HAL_UART_IT()` 传输下一个字符串之前，先传输每个字符串，我们等待传输完成。然而，这是轮询模式下 `HAL_UART()` 的变体，因为我们每次传输都有忙等。

如果速度对你的应用程序没有严格要求，且 `HAL_UART()` 的使用限于应用程序的少数部分，代码可以像示例 15 所示进行重新排列。该示例是针对 STM32F4 的。请参考书中针对你的 Nucleo 的示例。

![](img/9ef247bc7328ae96d937b3818a681558_228_0.png)

## 通用异步串口通信

本书的范围。

使用环形缓冲区（circular buffer），我们可以按照以下方式定义一个新的 UART 发送函数：

文件名：`src/main-ex3.c`

```c
uint8_t UART_Transmit(UART_HandleType *huart, uint8_t *pData, uint16_t len) {
    if (HAL_UART_Transmit_IT(huart, pData, len) != HAL_OK) {
        if (RingBuffer_Write(&xbuf, pData, len) != RING_BUFFER_OK) {
            return 0;
        }
    }
    return 1;
}
```

该函数做了两件事：它尝试在中断模式下将缓冲区发送到 UART；如果 `HAL_UART_Terminate_IT` 失败（这意味着 UART 正在发送另一个消息），则将该序列放置在环形缓冲区内。

由 `HAL_UART_TxCompleteCallback()` 来检查环形缓冲区中的待处理字节：

文件名：`src/main-ex3.c`

```c
void HAL_UART_TxCompleteCallback(UART_HandleType *huart) {
    if (RingBuffer_GetDataLength(&xbuf) > 0) {
        RingBuffer_Read(&xbuf, &xData, 1);
        HAL_UART_Transmit_IT(huart, &xData, 1);
    }
}
```

现在可以通过执行忙等待（busy-wait）来安排 `printWelcomeMessage()` 和 `processUserInput()` 函数，如下所示：

文件名：`src/main-ex3.c`

```c
void printWelcomeMessage() {
    char *strings[] = {"\u001b[0H;\u001b[2J", "WELCOME_MSG, MAIN_MENU, PROMPT?"};
    for (uint8_t i = 0; i < 5; i++) {
        UART_Transmit(&hu2, strings[i], strlen(strings[i]));
    }
}

uint8_t processUserInput(uint8_t input) {
    char msg[30];
    if(input || input > 3) {
        return 0;
    }
    sprintf(msg, "%d", input);
    UART_Transmit(&hu2, msg, strlen(msg));
}
```

## 通用异步串口通信

```c
switch(opt) {
    case 1:
        HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
        break;
    case 2:
        printf(msg, "\r\nUSER BUTTON status: %s",
        HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13) == GPIO_PIN_RESET ? "PRESSED" : "RELEASED");
        UART_Transmit(&huart2, (uint8_t*)msg, strlen(msg));
        break;
    case 3:
        return 2;
    }
UART_Transmit(&huart2, (uint8_t*)PROMPT, strlen(PROMPT));
return 1;
```

`RingBuffer_Read()` 的速度在性能更高的实现中可能无法达到理想状态。对于现实情况，`HAL_UART_TxCpltCallback`（来自 ISR 路由）的整个开销可能太高。如果这是你的情况，你可以考虑创建一个如下的函数：

```c
void processPendingTxTrans(UART_HandleTypeDef *huart) {
    if(RingBuffer_GetDataLen(txBuf) > 0) {
        RingBuffer_Read(&txBuf, &xtData, 1);
        HAL_UART_Transmit(huart, &xtData, 1);
    }
}
```

然后，你可以在主应用程序代码中或在使用 RTOS 的低权限任务中调用此函数。

## 8.5 错误管理

在处理外部通信时，错误管理是我们强烈建议考虑的一个方面。STM32 UART 外设提供了一些与通信错误相关的标志。此外，还可以启用相应的中断以便在错误发生时收到通知。

CubeHAL 会自动检测错误条件并向我们警告。我们只需要在应用程序代码中实现 `HAL_UART_ErrorCallback()` 函数。在发生错误时，`HAL_UART_IRQHandler()` 将自动调用它。要了解发生了哪种错误，我们可以检查 `UART_HandleTypeDef->ErrorCode` 字段的值。错误代码列表列于表 8.7。

## 通用异步串口通信

### 表 8.7：UART_HandleTypeDef->ErrorCode 的可能值列表

| UART 错误代码 | 描述 |
| --- | --- |
| `HAL_UART_ERROR_NONE` | 未发生错误 |
| `HAL_UART_ERROR_PE` | 校验检查错误 |
| `HAL_UART_ERROR_NE` | 噪声错误 |
| `HAL_UART_ERROR_FE` | 帧错误 |
| `HAL_UART_ERROR_ORE` | 溢出错误 |
| `HAL_UART_ERROR_DMA` | DMA 传输错误 |

`HAL_UART_Handler()` 的设计使我们不需要关心 UART 管理的实现细节。HAL 代码将执行处理错误所需的所有步骤（例如清除事件标志、挂起位等），将处理错误的责任留给应用层（例如，我们可以要求对端重新发送受损坏的帧）。

## 8.6 HAL_UART 模块中的可用回调函数列表

到为止，我们已经看到了如何利用回调机制接收事件通知。CubeHAL 采用事件驱动方法设计，所有的回调函数都与 UART 相关。对于大多数 HAL 模块，可以在 `Core/Inc/stm32fxx_hal_conf.h` 中将宏 `USE_PPP_REGISTER_CALLBACKS` 设置为 1（其中 PPP 是相应的外设）。这将启用这些函数。最后两个回调与 UART 模块的 FIFO 关，即 `HAL_UART_MspInitCallback` 和 `HAL_UART_MspDeInitCallback`。

## 表 8.8：hal_uart 模块

| HAL_UART 回调 | 描述 |
| --- | --- |
| `HAL_UART_TxHfcCallback` | 发送完成回调 |
| `HAL_UART_TxCompleteCallback` | 发送完成回调 |
| `HAL_UART_RxHfcCallback` | 接收完成回调 |
| `HAL_UART_RxCompleteCallback` | 接收完成回调 |
| `HAL_UART_ErrorCallback` | 错误回调 |
| `HAL_UART_AbortCallback` | 中止回调 |
| `HAL_UART_AbortTransmitCallback` | 中止发送回调 |
| `HAL_UART_AbortReceiveCallback` | 中止接收回调 |
| `HAL_UART_MspInitCallback` | UART 初始化 |
| `HAL_UART_MspDeInitCallback` | UART 反初始化 |
| `HAL_UARTEX_WakeupCallback` | 唤醒回调 |
| `HAL_UARTEX_RxFifoFullCallback` | 接收 FIFO 满回调 |
