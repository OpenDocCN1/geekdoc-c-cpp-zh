
## 8.2 使用 CubeMX 配置 USART

如你所示，该函数的设计适用于应用程序内部使用的每个 USART。如果该语句规定了给定 USART（在我们的例中为 `USART2`）的初始化代码，其余代码配置了 `PA2` 和 `PA3` 引脚。**请注意，复用功能可能会根据配备 Nucleo 板的 MCU 而变化。** 请参考书籍示例查看适用于你的 Nucleo 的正确初始化代码。

一旦我们配置了 `USART2` 接口，就可以开始与 PC 交换消息了。

> 请注意，之前提供的代码不足以初始化 STM32 MCU 的 USART 外设。某些 STM32 微控制器（如 `STM32F334R8`）允许开发者为任何外设选择时钟源（例如，`STM32F334R8` MCU 中的 USART 可以选择从 `SYSCLK`、`HSI`、`HSE` 或 `PCLK` 时钟）。强烈建议在第一次为你的 MCU 配置外设时使用 CubeMX，并仔细检查生成的代码以寻找此类异常。

| F334 | F303 |
| :--- | :--- |

## 8.2.1 使用 CubeMX 配置 USART

如你所示，该函数的设计适用于应用程序内部使用的每个 USART。如果该语句规定了给定 USART（在我们的例中为 `USART2`）的初始化代码，其余代码配置了 `PA2` 和 `PA3` 引脚。**请注意，复用功能可能会根据配备 Nucleo 板的 MCU 而变化。** 请参考书籍示例查看适用于你的 Nucleo 的正确初始化代码。

一旦我们配置了 `USART2` 接口，就可以开始与 PC 交换消息了。

> *某些用户，特别是拥有 Nucleo-F3 的用户，会注意到配置页面包含更多设置，位于 `stm32XXX_hal_msp.c` 文件。请参考目标 MCU 的参考手册获取更多信息。

# 通用异步串口通信

![](img/9ef24bc7328ae96d937b381a681558_217_0.png)

图 5：CubeMX 用于轻松配置 USART 接口

## 8.3 轮询模式下的 UART 配置

一旦我们配置了 `USART2` 接口，就可以开始与 PC 交换消息了。有几种方法处理数据传输和接收：轮询、中断和 DMA。

### 轮询模式

在轮询模式下，CPU 等待 USART 操作完成。这是最简单的方法，但效率最低。

在轮询模式下通过 USART 传输字节序列，HAL 提供了函数：

```
HAL_StatusTypeDef HAL_UART_Transmit(UARTHandleTypeDef* huart, uint8_t *pData, uint16_t Size, uint32_t Timeout);
```

其中：

- `huart` 是指向之前看到的 USART 实例的指针，识别并配置 USART 外设。
- `pData` 是指向数组的指针，长度与 `Size` 参数相同，包含要传输的字节序列。
- `Timeout` 是在完成前愿意等待的最大时间（毫秒）。如果传输未在规定时间内完成，函数将中止并返回 `HAL_TIMEOUT` 值。

在轮询模式下通过 USART 接收字节序列，HAL 提供了函数：

```c
HAL_StatusTypeDef HAL_UART_Receive(UARTHandleTypeDef* huart, uint8_t *pData, uint16_t Size, uint32_t Timeout);
```

其中：

- `huart` 是指向之前看到的 USART 实例的指针，识别并配置 USART 外设。
- `pData` 是指向数组的指针，长度与 `Size` 参数相同，包含要接收的字节序列。
- `Timeout` 是在完成前愿意等待的最大时间（毫秒）。如果接收未在规定时间内完成，函数将中止并返回 `HAL_TIMEOUT` 值。

> 需要注意的是，这两个函数提供的超时机制仅在由 CubeMX 生成的代码每 1ms 调用一次 `HAL_IncTick()` 例程时才有效（增加 HAL 计数器的函数是在 SysTick 定时器中断服务程序 ISR 中调用的）。

好了。现在是时候看示例了。

文件名：`src/main-ex.c`

```c
int main(void) {
    uint8_t opt = 0;
    /* 重置所有外设，初始化 Flash 接口和 SysTick */
    HAL_Init();
    /* 配置系统时钟 */
    SystemClock_Config();
    /* 初始化所有配置好的外设 */
    MX_GPIO_Init();
    MX_USART2_UART_Init();

    printMessage:
    printWelcomeMessage();

    while (1) {
        opt = readUserInput(opt);
        processUserInput(opt);
        if(opt == 3)
            goto printMessage;
    }
}

void printWelcomeMessage(void) {
    HAL_UART_Transmit(&huart2, (uint8_t*)"\033[0;0H", strlen("\033[0;0H"), HAL_MAX_DELAY);
    HAL_UART_Transmit(&huart2, (uint8_t*)"\033[2J", strlen("\033[2J"), HAL_MAX_DELAY);
    HAL_UART_Transmit(&huart2, (uint8_t*)WELCOME_MSG, strlen(WELCOME_MSG), HAL_MAX_DELAY);
    HAL_UART_Transmit(&huart2, (uint8_t*)MAIN_MSG, strlen(MAIN_MSG), HAL_MAX_DELAY);
}

uint8_t readUserInput(void) {
    char readBuf[1];
    HAL_UART_Transmit(&huart2, (uint8_t*)PROMPT, strlen(PROMPT), HAL_MAX_DELAY);
    HAL_UART_Receive(&huart2, (uint8_t*)readBuf, 1, HAL_MAX_DELAY);
    return atoi(readBuf);
}

uint8_t processUserInput(uint8_t opt) {
    char msg[30];

    if(!opt || opt > 3) {
        return 0;
    }

    sprintf(msg, "%d", opt);
    HAL_UART_Transmit(&huart2, (uint8_t*)msg, strlen(msg), HAL_MAX_DELAY);

    switch(opt) {
        case 1:
            HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
            break;
        case 2:
            sprintf(msg, "\r\nBUTTON STATUS: %s",
                    HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13) == GPIO_PIN_RESET ? "PRESSED" : "RELEASED");
            HAL_UART_Transmit(&huart2, (uint8_t*)msg, strlen(msg), HAL_MAX_DELAY);
            break;
        case 3:
            return 2;
    }

    return 0;
}
```

该示例是一个简单的裸机控制台。应用程序开始打印欢迎消息（第 36 行），然后进入循环等待用户选择。第一个选项允许切换 LD2 LED，第二个选项允许读取 USER 按钮的状态。最后，是那个会导致打印欢迎屏幕的选项。

> 两个 `"\033[0;H"` 和 `"\033[2J"` 是转义序列。它们是用于操作终端的标准字符序列。

为了与这个简单的控制台交互，我们需要一个串口通信程序。简单的方法是在 Windows 平台使用如 `putty` 的独立程序（如果你有 Windows 版本，也可以考虑使用 HyperTerminal），或者在 Linux 和 MacOS 使用 `kermit`。然而，现在 STM32CubeIDE 引入了集成串口工具。

## 8.3.1 为 Eclipse 安装 Terminal 插件

Eclipse 提供了一个方便的跨平台插件，可以在 IDE 内部添加终端模拟器，而无需额外工具。该插件在 Eclipse Marketplace 中免费提供。

要安装插件，前往 `Help` -> `Eclipse Marketplace...`。在文本框中输入 "terminal"。过一会儿，Terminal 插件就会出现，如图 8.6 所示。点击 `Install` 按钮并按照要求重启 Eclipse。

![](img/9ef247bc7328ae6d937b381a681558_0.png)
图 8.6: Eclipse Marketplace

要打开终端面板，可以按下 `Ctrl+Alt+T`，或者点击 Eclipse 工具栏上的专用图标，如图 8.7 所示。

![](img/9ef247bc7328ae6d937b381a681558_1.png)
图 8.7: 如何启动终端

出现 Launch Terminal 对话框，选择 Serial Terminal 类型（见图 8.8），然后选择对应 Nucleo 的 COM 口并在 CubeMX 中设置波特率。点击 `OK` 按钮。

![](img/9ef247bc7328ae6d937b381a681558_0.png)
图 8.8: 类型选择

现在你可以重置 Nucleo。使用 HAL 库编写的控制台应该出现在串口控制台中，如图 8.9 所示。

![](img/9ef247bc7328ae6d937b381a681558_1.png)
图 8.9: 终端中的 Nucleo 控制台
