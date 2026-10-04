
| TIM_TRGO_RESET | 当 `TIM->EGR` 寄存器的 `UG` 位被设置时生成 TRGO 信号。更多信息见 11.3.3 节 |
| --- | --- |
| TIM_TRGO_ENABLE | 当主定时器启用时生成 TRGO 信号。这对于同时启动多个定时器或配置启用从机定时器的窗口用 |
| TIM_TRGO_UPDATE | 选择更新事件作为触发输出 (TRGO)。例如，主定时器可以作为从机定时器的分频器（我们在 11.3.1.2 节中学习过这种模式） |
| TIM_TRGO_OC1 | 一旦发生捕获或比较匹配，触发输出发送正脉冲 |

表 11.14：从机模式下定时器可用的触发/时钟源

| 定时器主模式选择 | 描述 |
| --- | --- |
| TIM_TRGO_OC1REF | 通道1 发生捕获或比较匹配时，触发输出发送脉冲 |
| TIM_TRGO_OC2REF | 通道2 发生捕获或比较匹配时，触发输出发送脉冲 |
| TIM_TRGO_OC3REF | 通道3 发生捕获或比较匹配时，触发输出发送脉冲 |
| TIM_TRGO_OC4REF | 通道4 发生捕获或比较匹配时，触发输出发送脉冲 |

```c
sSlaveConfig.SlaveMode = TIM_SLAVE_TRIGGER;
sSlaveConfig.InputTrigger = TIM_TS_ITFP1;
sSlaveConfig.TriggerPolarity = TIM_TRIGGERPOLARITY_RISING;
sSlaveConfig.TriggerFilter = 15;
HAL_TIM_SlaveConfigSynchron(&htim1, &sSlaveConfig);

sMasterConfig.OutputTrigger = TIM_TRGO_UPDATE;
sMasterConfig.SlaveMode = TIM_MASTERSLAVEMODE_ENABLE;
HAL_TIM_MasterConfigSynchronization(&htim1, &sMasterConfig);
}

void MX_TIM3_init(void) {
    TIM_SlaveConfigTypeDef sSlaveConfig;

    htim3.Instance = TIM3;
    htim3.Init.Prescaler = 0;
    htim3.Init.CounterMode = TIM_COUNTERMODE_UP;
    htim3.Init.Period = 1;
    htim3.Init.ClockDivision = TIM_CLOCKODIVISION_DIV1;
    HAL_TIM_BaseInit(&htim3);

    sSlaveConfig.SlaveMode = TIM_SLAVEMODE_EXTERNAL1;
    sSlaveConfig.InputTrigger = TIM_TS_ITR0;
    HAL_TIM_SlaveConfigSynchro(&htim3, &sSlaveConfig);

    HAL_NVIC_SetPriority(TIM3_IRQ, 0, 0);
    HAL_NVIC_EnableIRQ(TIM3_IRQ);
}
```

```c
void HAL_TIM_Base_MInit(TIM_HandleTypeDef* hbase) {
    GPIO_InitTypeDef GPIO_InitStruct;
    if(hbase->Instance==TIM3) {
        __HAL_RCC_TIM3_CLK_ENABLE();
    }

    if(hbase->Instance==TIM1) {
        __HAL_RCC_TIM1_CLK_ENABLE();

        GPIO_InitStruct.Pin = GPIO_PIN_8;
        GPIO_InitStruct.Mode = GPIO_MODE_PP;
        GPIO_InitStruct.Pull = GPIO_PULLDOWN;
        GPIO_InitStruct.Speed = GPIO_SPEED_LOW;
        GPIO_InitStruct.Alternate = GPIO_AF2_TIM1;
        HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);
    }
}
```

# 定时器

第 [29:38] 行配置 `TIM1` 使用内部 APB 总线时钟。第 [40:44] 行将 `TIM1` 配置为从模式，使得当 `TI1FP` 线变为高电平时它开始计数（即：被触发）。`PA8` GPIO 在第 [74:79] 行中配置（配置为 `GPIO_AF2_TIM1`）。注意，第 76 行激活了内部下拉电阻：这可以防止浮空输入意外触发定时器。出于相同的原因，第 43 行将触发滤波器（`TriggerFilter`）设置为最大值（如果你尝试将其设置为零，你会发现很容易意外触发，即使仅仅是触摸连接到 `PA8` 引脚的线）。

第 [46:48] 行将 `TIM1` 同时配置为主模式。每当产生更新事件时，定时器都会触发其内部线路（该线连接到 `TIM3` 的 `IT0` 线）。最后，第 [61:63] 行将 `TIM1` 配置为外部时钟模式，选择 `IT0` 线作为时源。

> 注意，在我们的案例中 `LD2` LED 每 500ms 闪烁一次（2Hz），`TIM1` 的周期被设置为 249³，这导致 `TIM1` 的更新频率为 4Hz。这是因为根据应用公式 [3]，我们得到：
>
> $$UpdateEvent = \frac{4Hz}{(0+1)(1+1)(0+1)} = 2Hz = 0.5s$$
>
> 记住周期（`Period`）字段不能设置为零。

要触发 `TIM1`，你必须将 `PA8` 引脚连接到 +3V 源。图 11.12 显示了如何在 Nucleo-F072 中进行连接。

²³ 显然，该预分频值指的是运行在 48MHz 下的 STM32F07RB MCU。对于你的 Nucleo，请检查书籍示例以获取正确的预分频设置。

![](img/9ef247bc7328ae96d937b3818a681558_325_0.png)

### 11.3.2.1 启用触发相关中断

当定时器在从模式下工作时，每当指定的触发事件发生，如果已启用，就会产生定时器 IRQ。例如，当主时钟由于更新事件被触发时，从模式定时器的 IRQ 会触发，我们可以通过定义以下回调函数来通知此：

```c
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim) {
    // 回调实现
}
```

### 11.3.4 计数模式

```c
htim3.Instance = TIM3;
htim3.Init.Prescaler = 65535;
htim3.Init.CounterMode = TIM_COUNTERMODE_UP;
htim3.Init.Period = 120;
htim3.Init.ClockDivision = TIM_CLOCKODIV_DIV1;
HAL_TIM_BaseInit(&htim3);
```

```c
sClockSourceConfig.ClockSource = TIM_CLOCKSOURCE_INTERNAL;
HAL_TIM_ConfigClockSource(&htim3, &sClockSourceConfig);
```

```c
sMasterConfig.MasterOutputTrigger = TIM_TRGO_RESET;
sMasterConfig.MasterSlaveMode = TIM_MASTERSLAVEMODE_ENABLE;
HAL_TIM_X_MasterConfigSynchronization(&htim3, &sMasterConfig);
```

定时器

300

![](img/9ef247bc7328ae96d937b3818a681558_329_0.png)

相反，当定时器在 `TIM_COUNTERMODE_CENTRALIGNED` 模式下计数时，它从零开始计数到 `Period` 值：这会导致触发定时器中断（IRQ）并设置 `UIF` 标志（即产生更新事件并由 HAL 调用 `HAL_PeriodElapsedCallback()` 函数）。随后，定时器开始倒计数到零，并产生另一个更新事件（以及相应的中断）。

## 13.5 输入捕获模式

通用定时器的设计目的并不是为了作为时间基准发生器。尽管完全可以使用它们来完成这项工作，但也可以使用基础定时器和 `SysTick` 等定时器来执行此任务。通用定时器提供了更先进的功能，可用于驱动其他与其他相关的活动。

图 11.16 显示了通用定时器中输入通道的结构。如你所见，每个输入都连接到一个边缘检测器，该检测器还配备了滤波器以对输入信号进行“去抖”。边缘检测器的输出进入源复用器（`IC1`、`IC2` 等）。这允许在给定的 I/O 分配给另一个外设时，“重映射”输入通道。最后，一个专用的分频器允许“减慢”输入信号的频率，以匹配无法降低的定时器运行频率（稍后我们将看到）。

> 某些通用定时器（例如 `TIM14`）的输入通道较少，因此输入阶段结构也较简单。请参考你的 MCU 参考手册以了解你将要使用的定时器的具体结构。

## 定时器

301

![](img/9ef247bc7328ae96d937b3818a681558_330_0.png)

图 11.16：通用定时器输入的捕获模式

![](img/9ef247bc7328ae96d937b3818a681558_330_1.png)

图 11.17：输入定时器通道的外部信号采集过程

图 11.17 显示了捕获过程的工作原理。`TIMx` 是一个定时器，配置为以给定的 `TIMx CLK` 时钟频率⁷ 运行。这意味着每隔 `TIMx_CLK` 秒，`TIMx_CNT` 寄存器就会递加到 `Period` 值。假设我们在一侧应用一个方波信号，并配置定时器在输入信号的每个上升沿触发

> ⁷ 定时器频率频率独立于定时器的工作方式（在此情况下为输入捕获模式）。如前文所述，定时器频率取决于总线频率或外部时源以及相关的分频器设置。

`TIMx_CCRx` 寄存将在每次检测到跳变时用 `TIMx_CNT` 寄存器的内容更新。当这种情况发生时，定时器将产生相应的中断或 DMA 请求，以便跟踪计数器值。

为了获取外部信号，需要连续两次捕获。周期通过减去这两个值——`CNT₀`（图 11.17 中的值 4）和 `CNT₁`（图 11.17 中的值 20）并使用以下公式计算：

```
$Period = Capture \cdot \left( \frac{TIMx_CLK}{(Prescaler + 1)(CHPrescaler)(PolarityIndex)} \right) [4]$
```

其中：

$Capture = CNT₀ - CNT₁$ 如果 $CNT₀ < CNT₁$

$Capture = TIMx\_Period - CNT₀ + CNT₁$ 如果 $CNT₀ > CNT₁$

$CHPrescaler$ 是可以应用到输入通道的进一步分频器，$PolarityIndex$ 如果配置为在输入信号的上升沿或下降沿触发，则等于 1；如果两个边缘都进行采样，则等于 2。

另一个相关条件是 UEF 频率应该低于采样信号频率。这之所以重要显而易见：如果定时器的运行速度比采样的信号快，那么它在能够采样信号边缘之前就会溢出（即 `Period` 计数耗尽，见图 11.18）。对于这种情况，通常方便将 `Period` 值设置为最大值，并增加分频器系数以降低计数频率。

![](img/9ef247bc7328ae96d937b3818a681558_331_0.png)

图 11.18：如果我们使用的输入通道使用了采样信号，那么它将在两次捕获之前溢出

为了配置输入通道，我们使用 `HAL_TIM_IC_ConfigChannel()` 函数和 `TIM_InitTypeDef` 结构体，其定义如下：

```c
typedef struct {
    uint32_t Polarity;     /** 指定输入信号的边缘。 */
    uint32_t Selection;    /** 指定选择。 */
    uint32_t Prescaler;    /** 指定分频器。 */
    uint32_t Filter;        /** 指定滤波器。 */
} TIM_InitTypeDef;
```

* `Polarity`：指定输入信号的边缘。
* `Selection`：指定的选择。
* `Prescaler`：是可以应用到输入通道的进一步分频器。
* `Filter`：是指定的滤波器。

现在是时候看一个实际示例了。我们将通过 `TIM3` 的通道 1（STM32F0 中的引脚 `PA6`）对 `LD2`（连接到 LED 的引脚）的切换频率进行采样。我们将通道 1 配置为输入捕获引脚，并配置为 DMA 模式，以触发 DMA 请求，自动填充在检测到上升沿时存储 `TIM3_CNT` 的缓冲区。

在分析 `main()` 函数之前，最好查看 `TIM3` 的初始化例程。

```c
/* TIM3 初始化函数 */
void MX_TIM3_Init(void) {
    TIM_InitTypeDef sConfig;

    htim3.Instance = TIM3;
    htim3.Prescaler = 999;
    htim3.CounterMode = TIM_COUNTER_UP;
    htim3.Period = 65535;
    htim3.ClockDivision = TIM_CLOCK_DIVISION_DIV1;
    HAL_TIM_IC_Init(&htim3);

    sConfig.Polarity = TIM_INPUTCHANNEL_POLITY_RISING;
    sConfig.Selection = TIM_SELECTION_DIRECTTI;
    sConfig.Prescaler = TIM_ICPSC_DIV1;
    sConfig.Filter = 0;
    HAL_TIM_IC_ConfigChannel(htim3, sConfig, TIM_CHANNEL_1);
}

void HAL_TIM3_MspInit(TIM_HandleTypeDef* htmic) {
    GPIO_InitTypeDef GPIO0_InitStruct;
    if (htimic->Instance == TIM3) {
        /* 外设时钟启用 */
        __HAL_RCC_TIM3_CLK_ENABLE();
        /*TIM3 GPIO 配置 */
        PA6 -----------> TIM3_CHI
        */
        GPIO0_InitStruct.Pin = GPIO_PIN_6;
        GPIO0_InitStruct.Mode = GPIO_MODE_AF_PP;
        HAL_GPIO_Init(GPIOA, &GPIO0_InitStruct);
    }
}
```

# 定时器

```c
GPIO_InitStruct.Pull = GPIO_NOPULL;
GPIO_InitStruct.Speed = GPIO_SPEED_LOW;
GPIO_InitStruct.Alternate = GPIO_AF1_TIM3;
HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);
/* 外设 DMA 初始化/ */
hdma_tim3_ch1_Init.Instance = DMA1_Channel4;
hdma_tim3_ch1_Init.Direction = DMA_PERIP_TO_MEMORY;
hdma_tim3_ch1_Init.PeriphInc = DMA_PINC_DISABLE;
hdma_tim3_ch1_Init.MemInc = DMA_MINC_ENABLE;
hdma_tim3_ch1_Init.DataAlignment = DMA_PDATAALIGN_HALFWORD;
hdma_tim3_ch2_Init.MemDataAlignment = DMA_MDATAALIGN_HALFWORD;
hdma_tim3_ch2_Init.Mode = DMA_NORMAL;
hdma_tim3_ch1_Init.Priority = DMA_PRIORITY_LOW;
HAL_DMA_Init(&hdma_tim3_ch1);
/* 外设 DMA 句柄指向同一个 DMA 句柄 *
请注意，只有一个通道用于执行所有请求的 DMA。 */
_HAL_LINKDMA(htim_ic, hdma_TIM_ID_CC1, hdma_tim3_ch1_trig);
```

![](img/9ef247bc7328ae96d937b3818a681558_334_0.png)

图 11.19: 如何在 Nucleo-F02RB 中连接 `PA5` 和 `PA6` 引脚
