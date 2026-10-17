
相反，第二种模式只需通过使用外部时钟源即可激活。这允许使用更精确和专用的源，并最终进一步降低计数频率。事实上，当选择外部时钟源模式 2 时，计算更新事件的公式为：

```
EXT_clock / ((Prescaler + 1) * (Period + 1))
```

其中 `EXT_clock` 是外部源频率，`Prescaler` 是通过以下 `TIMConfigTypeDef` 结构体定义的：

```c
typedef struct {
    uint32_t ClockSource;  /* 时钟源 */
    uint32_t Polarity;      /* 极性 */
    uint32_t Prescaler;   /* 分频器 */
    uint32_t Filter;       /* 滤波器 */
} TIMConfigTypeDef;
```

- `ClockSource`：用于定时器的时钟源。其参见第 11.7 节，默认为 `TIM_CLOCK_SOURCE_INTERNAL`。
- `Polarity`：用于定时器的时钟极性。其参见第 11.8 节，默认为 `TIM_CLOCK_POLARITY_NONINVERTED`。
- `Prescaler`：外部时钟的分频器。其参见第 11.9 节，默认为 `TIM_CLOCKPRESCALER_DIV1`。
- `Filter`：该字段定义了信号的滤波器。

#### 表 11.7：可用时钟源

| 时钟源 | 描述 |
| :--- | :--- |
| `TIM_CLOCK_SOURCE_INTERNAL` | 由 APB 总线驱动 |
| `TIM_CLOCK_SOURCE_ETRMODE1` | 当定时器被配置为从模式时可用 |
| `TIM_CLOCK_SOURCE_ETRMODE2` | 由外部源驱动 |

#### 表 11.8：可用时钟极性

| 时钟极性 | 描述 |
| :--- | :--- |
| `TIM_CLOCK_POLARITY_NONINVERTED` | 在外部源的上升沿同步 |
| `TIM_CLOCK_POLARITY_INVERTED` | 在外部源的下降沿同步 |
| `TIM_CLOCK_POLARITY_BOTH` | 在外部源的上升沿和下降沿同步 |

#### 表 11.9：可用时钟分频器

| 时钟分频器 | 描述 |
| :--- | :--- |
| `TIM_CLOCKPRESCALER_DIV1` | 无分频 |
| `TIM_CLOCKPRESCALER_DIV2` | 每 2 次事件捕捉一次 |
| `TIM_CLOCKPRESCALER_DIV4` | 每 4 次捕捉一次 |
| `TIM_CLOCKPRESCALER_DIV8` | 每 8 次捕捉一次 |

让我们构建一个示例，展示如何为 TIM3 使用外部时钟。MCO 引脚已启用并连接到 HSI 时钟。以下代码显示了示例中相关的元素。

文件名：`Core/Src/main-ex3.c`

```c
void MX_TIM3_Init(void) {
    TIM_ClockConfigTypeDef sClockSourceConfig;

    htim3.Instance = TIM3;
    htim3.Init.Prescaler = 999;
    htim3.Init.CounterMode = TIM_COUNTERMODE_UP;
    htim3.Init.Period = 3999;
    htim3.Init.ClockDivision = TIM_CLOCKDIVISION_DIV1;
    htim3.Init.RepetitionCounter = 0;
    HAL_TIM_Base_Init(&htim3);

    sClockSourceConfig.ClockSource = TIM_CLOCK_SOURCE_ETRMODE2;
    sClockSourceConfig.Polarity = TIM_CLOCK_POLARITY_NONINVERTED;
    sClockSourceConfig.Prescaler = TIM_CLOCKPRESCALER_DIV1;
    sClockSourceConfig.Filter = 0;
    HAL_TIM_ConfigClockSource(&htim3, &sClockSourceConfig);

    HAL_NVIC_SetPriority(TIM3_IRQn, 0, 0);
    HAL_NVIC_EnableIRQ(TIM3_IRQn);
}

void HAL_TIM_Base_MspInit(TIM_HandleTypeDef* htim_base) {
    GPIO_InitTypeDef GPIO_InitStruct;
    if(htim_base->Instance == TIM3) {
        /* 外设时钟使能 */
        __HAL_RCC_TIM3_CLK_ENABLE();
        __HAL_RCC_GPIOD_CLK_ENABLE();
        /** TIM3 GPIO Configuration
        PD2     ---> TIM3_ETR
        */
        GPIO_InitStruct.Pin = GPIO_PIN_2;
        GPIO_InitStruct.Mode = GPIO_MODE_AF_PP;
        GPIO_InitStruct.Pull = GPIO_NOPULL;
        GPIO_InitStruct.Speed = GPIO_SPEED_LOW;
        HAL_GPIO_Init(GPIOD, &GPIO_InitStruct);
    }
}
```

第 [27:33] 行配置 TIM3 定时器，将其预分频设置为 999，周期设置为 3999。第 [34:38] 行配置连接到 TIM3 的外部源。HSI 振荡器运行在 8MHz²，根据公式 [2] 我们可以计算 UE 频率，其等于：

$$UpdateEvent = \frac{8000000}{(999+1)(3999+1)} = 2Hz = 0.5s$$

最后，第 [48:58] 行启用 TIM3 并将 PD2 引脚（对应于 TIM3_ETR 引脚）配置为输入源。

> **注意**
>
> 需要注意的是，在将 GPIO 端口作为 TIM3 的时钟源之前，必须使用 `__HAL_RCC_GPIOD_CLK_ENABLE()` 宏启用它。这同样适用于 TIM3，它通过使用 `__HAL_RCC_TIM3_CLK_ENABLE()` 启用：这是因为外部时钟并不是直接馈送到预分频器，而是首先通过专用逻辑由 APBx 时钟同步。

### 11.3.1.2 外部时钟模式 1

STM32 通用和高级定时器可以配置为主从模式¹。当配置为从模式时，定时器可以通过内部 ITR0、ITR1、ITR2 和 ITR3 线供电，或者连接到 TI1FP1 或 TI2FP2 源（对应通道 1 和 2 输入引脚）的外部时钟。这种工作模式被称为外部时钟模式 1。

¹ 此 HSI 频率与 STM32F072RB 相关。在其他 STM32 MCU 中，HSI 速度为 16MHz。请咨询您的 MCU 数据手册并相应调整计算。

² 正如我们将看到的，定时器可以同时配置为主模式和从模式。

外部时钟模式 1 和 2 对于所有 STM32 平台的初学者来说都相当困惑。两种模式都是一种使用外部时源为定时器时钟的方法，但第一种通过将定时器配置为从模式来实现（这确实是一种“触发”形式），而第二种通过简单地选择不同的时源来实现。我不知道这种命名的由来，但这种区别的实际效果是不同的。然而，重要的是，在 ETR 模式 1 和 ETR 模式 2 下配置定时器的方法完全不同，正如下一个示例中所示。

观察图 11.16 可以看到，TI1FP1 和 TI2FP2 只是输入滤波器作用后定时器的 TI1 和 TI2 输入通道。

为了在从模式下配置定时器，我们使用 `HAL_TIM_SlaveConfigSync()` 函数和 `TIM_SlaveConfigTypeDef` 结构体实例，其定义如下：

```c
typedef struct {
    uint32_t SlaveMode;               /* 从模式选择 */
    uint32_t InputTrigger;            /* 输入触发源 */
    uint32_t TriggerPolarity;         /* 输入触发极性 */
    uint32_t TriggerPrescaler;        /* 输入触发预分频器 */
    uint32_t TriggerFilter;           /* 输入触发滤波器 */
} TIM_SlaveConfigTypeDef;
```

- `SlaveMode`：当定时器配置为从模式时，它可以被多个源时钟驱动/触发。此字段可以取表 11.10 中的值。本段介绍关于 `TIM_SLAVEMODE_EXTERNAL1` 模式。
- `InputTrigger`：定义在从模式下触发定时器时钟的源。它可以取表 11.11 中的值。
- `TriggerPolarity`：指示触发/时钟源的极性。它可以取表 11.12 中的值。
- `TriggerPrescaler`：指定外部时钟源的预分频器。它可以取表 11.13 中的值。默认选择 `TIM_TRIGGERPRESCALER_DIV1`。
- `TriggerFilter`：此 4 位字段定义了采样连接到输入引脚的外部时钟/触发信号的频率，以及应用到它的数字滤波器长度。数字滤波器由一个事件计数器组成，需要 N 个连续事件来验证输出上的转换。请参阅您的 MCU 数据手册有关如何计算 fTS（死区时间信号）。默认情况下禁用滤波器。

#### 表 11.10：可用的从模式

| 从模式 | 工作模式 | 描述 |
| :--- | :--- | :--- |
| `TIM_SLAVEMODE_DISABLE` | 禁用 | 从模式被禁用（默认值） |
| `TIM_SLAVEMODE_RESET` | 触发 | 所选触发的上升沿初始化计数器并产生寄存器更新 |
| `TIM_SLAVEMODE_GATED` | 触发 | 当触发输入 (TRGI) 为高电平时启用计数器时钟 |
| `TIM_SLAVEMODE_TRIGGER` | 触发 | 触发输入的上升沿启动计数器 |
| `TIM_SLAVEMODE_EXTERNAL1` | 外部时钟模式 1 | 使用外部触发源作为时钟 |

如上一个示例所示，MCO 引脚被启用并连接到 HSI 时钟。以下代码显示了示例中最相关的部分。

文件名: `Core/Src/main-ex4.c`

```c
void MX_TIM3_Init(void) {
    TIM_SlaveConfigTypeDef sSlaveConfig;

    htim3.Instance = TIM3;
    htim3.Init.Prescaler = 999;
    htim3.Init.CounterMode = TIM_COUNTERMODE_UP;
    htim3.Init.Period = 3999;
    htim3.Init.ClockDivision = TIM_CLOCKDIVISION_DIV1;
    HAL_TIM_Base_Init(&htim3);

    sSlaveConfig.SlaveMode = TIM_SLAVEMODE_EXTERNAL1;
    sSlaveConfig.InputTrigger = TIM_TS_TI2FP2;
    sSlaveConfig.TriggerPolarity = TIM_TRIGGERPOLARITY_RISING;
    sSlaveConfig.TriggerPrescaler = TIM_TRIGGERPRESCALER_DIV1;
    sSlaveConfig.TriggerFilter = 0;
    HAL_TIM_SlaveConfigSync(&htim3, &sSlaveConfig);

    HAL_NVIC_SetPriority(TIM3_IRQn, 0, 0);
    HAL_NVIC_EnableIRQ(TIM3_IRQn);
}

void HAL_TIM_Base_MspInit(TIM_HandleTypeDef* htim_base) {
    GPIO_InitTypeDef GPIO_InitStruct;
    if(htim_base->Instance == TIM3) {
        /* 外设时钟使能 */
        __HAL_RCC_TIM3_CLK_ENABLE();
        __HAL_RCC_GPIOA_CLK_ENABLE();

        /* TIM3 GPIO Configuration
        PA7     ---> TIM3_CH2
        */
        GPIO_InitStruct.Pin = GPIO_PIN_7;
        GPIO_InitStruct.Mode = GPIO_MODE_AF_PP;
        GPIO_InitStruct.Pull = GPIO_NOPULL;
        GPIO_InitStruct.Speed = GPIO_SPEED_LOW;
        GPIO_InitStruct.Alternate = GPIO_AF1_TIM3;
        HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);
    }
}
```

行 [34:38] 在从机模式下配置 TIM3。输入触发器被设置为 TI2FP2，且定时器同步到输入信号的上升沿。最后，行 [54:59] 将 PA7 配置为 TIM3 第二个通道的输入引脚。

### 11.3.1.3 使用 CubeMX 配置通用定时器的时源

配置通用定时器的源是一场噩梦，特别是对于 STM32 平台的初学者来说。CubeMX 可以简化这一过程，尽管这需要良好地理解主从模式以及 ETR 模式 1 和 ETR 模式 2。

要在外部时钟模式 2 下配置定时器，只需在配置面板中选择 ETR2 为时钟源即可，如图 11.6 所示。

**图 11.6：如何从 IP 面板中选择 ETR2 模式**

一旦选择了时钟源，就可以从配置中设置外部时钟滤波器、极性和分频器，如图 11.7 所示。

**图 11.7：如何配置 ETR2 模式的定时器**

在模式 1 下，我们可以与从机配合，然后选择触发源（即从机的时钟源），如图 11.8 所示。

**图 11.8：如何从 IP 树选择 ETR1 模式**

一旦选择了时钟源，就可以在定时器配置对话框中设置其他配置参数。

### 11.3.2 主从同步

一旦主模式下的定时器通过专用输出（触发输出 TRGO）连接到从机模式的定时器，这些输出线被称为 ITR0、ITR1、ITR2 和 ITR3。主定时器可以提供时钟源（从而充当分频器 - 我们上一节学过）或触发从机定时器。

内部触发 (ITR) 线 ITR0、ITR1、ITR2 和 ITR3 位于定时器内部。某些 STM32 微控制器（特别是 STM32F3）提供了名为 TRGO1 和 TRGO2 的独立触发线。书中未显示这种情况。

TRGO 线连接到 TIM2 的 ITR0 线，如图 11.9 所示。

**图 11.9：TIM1 可以通过 ITR0 线驱动 TIM2**

配置为*从机*的定时器也可以作为另一个定时器的*主*，从而创建复杂的定时器网络。例如，**图 11.10** 显示了如何级联连接定时器，而 **图 11.11** 显示了定时器如何形成层级结构。注意 TIM1、TIM2 和 TIM3 内部通过相同的 ITR0 线互连。这允许根据同一事件（重置、更新等）同步多个定时器。

**图 11.10：主从模式的组合用于级联定时器**

**图 11.11：主从模式的组合允许层级结构配置 TIM**

要在主模式下配置定时器，我们使用 `HAL_TIMEx_MasterConfigSynchronization()` 函数和 `TIM_MasterConfigTypeDef` 结构体实例，其定义如下：

```c
typedef struct {
    uint32_t MasterOutputTrigger; /* 触发输出 (TRGO) */
    uint32_t MasterSlaveMode;     /* 主从模式选择 */
} TIM_MasterConfigTypeDef;
```

- `MasterOutputTrigger`：指定 TRGO 输出的行为，可以取表 11.14 中的值。
- `MasterSlaveMode`：用于启用/禁用定时器的主从模式。它可以取 `TIM_MASTERSLAVEMODE_ENABLE` 或 `TIM_MASTERSLAVEMODE_DISABLE` 值。

#### 表 11.14：主模式下定时器的触发输出选择

| 主模式选择 | 描述 |
| :--- | :--- |
| `TIM_TRGO_RESET` | 复位计数器的触发输出 (UG 位来自 TIMx_EGR) |
| `TIM_TRGO_ENABLE` | 使能计数器的触发输出 (CEN 位来自 TIMx_CR1) |
| `TIM_TRGO_UPDATE` | 更新事件的触发输出 (更新事件来自 TIMx_EGR) |
| `TIM_TRGO_OC1` | 输出比较 1 的触发输出 |
| `TIM_TRGO_OC2REF` | 输出比较 2 参考的触发输出 |
| `TIM_TRGO_OC3REF` | 输出比较 3 参考的触发输出 |
| `TIM_TRGO_OC4REF` | 输出比较 4 参考的触发输出 |
