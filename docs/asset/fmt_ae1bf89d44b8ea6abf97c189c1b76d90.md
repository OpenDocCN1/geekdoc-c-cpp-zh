
# 电源管理

文件名：`Core/Src/main_ext.c`

```c
int main(void) {

    char msg[30];

    HAL_Init();

    Nucleo_BSP_Init();

    /* 在访问 PWR 外设的寄存器之前，我们必须启用它 */

    HAL_RCC_PWR_CLK_ENABLE();

    while (1) {

        if (HAL_PWR_GET_FLAG(PWR_FLAG_SB)) {

            /* 如果 PWR_CSR 中的待机标志位设置，则重位将由
               * 待机模式产生 */

            sprintf(msg, "RESET after STANDBY mode\r\n");

            HAL_UART_Transmit(&huart2, (uint8_t*)msg, strlen(msg), HAL_MAX_DELAY);

            /* 我们必须明确清除标志位 */

            HAL_PWR_CLEAR_FLAG(PWR_FLAG_SB);

        }

        sprintf(msg, "MCU in run mode\r\n");

        HAL_UART_Transmit(&huart2, (uint8_t*)msg, strlen(msg), HAL_MAX_DELAY);

        while (HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13) == GPIO_PIN_SET) {

            HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);

            HAL_Delay(100);

        }

        HAL_Delay(200);

        sprintf(msg, "Entering in SLEEP mode\r\n");

        HAL_UART_Transmit(&huart2, (uint8_t*)msg, strlen(msg), HAL_MAX_DELAY);

        SleepMode();

        sprintf(msg, "Exiting from SLEEP mode\r\n");

        HAL_UART_Transmit(&huart2, (uint8_t*)msg, strlen(msg), HAL_MAX_DELAY);

        while (HAL_GPIO_ReadPin(GPIOC, GPIO_PIN_13) == GPIO_PIN_SET) {

            HAL_Delay(200);

        }

        sprintf(msg, "Entering in STOP mode\r\n");

        HAL_UART_Transmit(&huart2, (uint8_t*)msg, strlen(msg), HAL_MAX_DELAY);

        StopMode();

        sprintf(msg, "Exiting from STOP mode\r\n");
```

## 代码解析

第 21 行的宏 `__HAL_RCC_PWR_ENABLE()` 启用了 PWR 外设：在我们执行任何与电源管理相关的操作之前，必须启用 PWR 外设，即使只是为了检查 `PWR->CSR` 寄存器中的待机标志位。对于挣扎于电源管理的新手用户来说，这是一个令人头疼的问题源。

第 31 行检查待机标志位是否设置；如果是，则 MCU 在从待机模式退出后将进行复位。

第 33 行代表运行模式：`LD2` LED 将一直闪烁，直到我们按下连接到 `PC13` 的 Nucleo 按钮。

`main()` 函数中的剩余代码显示了在 USER 按钮的每次按下下的三种低功耗模式。

第 74-106 行定义了 `SleepMode()` 函数，用于将 MCU 置于睡眠模式。所有 GPIO 都配置为模拟模式，以减少未用 IO 的电流消耗（特别是标记为悬空引脚的 IO）。相应的外设被关闭，但 GPIO 外设除外：`PC13` GPIO 用于从低功耗模式恢复。`UART2` 接口和 `SysTick` 定时器也是如此，后者被停止以防止 MCU 在 1ms 后退出低功耗模式。

第 96 行的 `HAL_PWR_EnterSLEEPMode()` 函数将 MCU 置于睡眠模式，直到 USER 按钮被按下。

## SleepMode 函数实现

文件名：`Core/Src/main_ext.c`

```c
void SleepMode(void) {

    GPIO_TypeDef GPIOInitStruct;

    /* 禁用所有 GPIO 以降低功耗 */

    MX_GPIO_Deinit();

    /* 将用户按键配置为外部中断发生器 */

    HAL_RCC_GPIO_CLK_ENABLE();

    GPIOInitStruct.Pin = B1_Pin;

    GPIOInitStruct.Mode = GPIO_MODE_IT_RISING;

    GPIOInitStruct.Pull = GPIO_NOPULL;

    HAL_GPIO_Init(B1_Port, &GPIOInitStruct);

    HAL_UART_Deinit(&huart2);

    /* 挂起 Tick 以防止 Systick 中断增加唤醒 
       否则 Systick 中断将在 1ms 内（HAL 时间基准）唤醒设备 */

    HAL_SuspendTick();

    HAL_RCC_PWR_CLK_ENABLE();

    /* 请求进入 SLEEP 模式 */

    HAL_PWR_EnterSLEEPMode(0, PWR_SLEEPENTRY_WFI);

    /* 如果在进入睡眠模式前禁用了，则恢复 Tick 中断 */

    HAL_ResumeTick();

    /* 初始化 GPIO */

    MX_GPIO_Init();

    /* 初始化 UART2 */

    MX_UART2_Init();

}
```
