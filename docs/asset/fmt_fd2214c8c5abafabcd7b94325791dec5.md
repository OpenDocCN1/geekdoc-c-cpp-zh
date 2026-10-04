
上述代码显示了 `main()` 函数的内容，应该很容易理解。定时器在第 56 行启动，ADC 以 DMA 模式启动以从 ADC 进行三次采集。如果你运行该示例，你会看到三秒后 DMA 完成传输并设置了 `convCompleted` 变量：这三次转换每三秒会在 UART2 接口上打印一次。

## 12.2.9 外部事件驱动的转换

在某些 STM32 MCU 中，可以配置 EXTI 线来触发 A/D 转换。例如，在 STM32F40RE MCU 中，可以启用 EXTI 线 11 用于此类目的。这意味着连接在该路上的任何引脚（PA11、PB11 等）都是触发转换的有效源。请注意，不能同时使用 EXTI 线和定时器作为触发源。

## 12.2.10 ADC 校准

某些 STM32 系列（如 STM32F1/F3/L0/L4/G4）实现的 ADC 外设提供了自动校准程序，该程序驱动包括 ADC 上电/断电序列在内的所有校准序列。在此过程中，ADC 计算出一个 7 位校准因子，并在内部应用于 ADC 直到下次 ADC 断电。在校准过程中，应用程序不能使用 ADC，必须等待校准完成。校准是任何 ADC 操作之前的。它消除了由于工艺或带隙变化导致不同芯片之间可能偏移误差。用于单端输入转换的校准因子与用于分端输入转换的因子不同。

`HAL_ADC_Ex` 模块提供了三个用于 ADC 校准的函数。

```
HAL_ADCEx_Calibration_Start(ADCHandleTypeDef* hadc, uint32_t SingleDiff);
```

会自动执行校准程序。它必须在调用 `HAL_ADC_Init()` 之后且在使用任何 `HAL_ADC_Start_XXX()` 例程之前调用。传递参数 `ADC_SINGLE_ENDED` 则执行单端校准，传递参数 `ADC_DIFFERENTIAL` 则执行分端校准。

函数 `uint32_t HAL_ADCEx_Calibration_GetValue(ADCHandleTypeDef* hadc, uint32_t SingleDiff);` 用于检索计算出的校准值，而 `HAL_StatusTypeDef HAL_ADCEx_Calibration_SetValue(ADCHandleTypeDef* hadc, uint32_t SingleDiff, uint32_t CalibrationFactor);` 用于设置自定义校准值。更多信息，请参考你所考虑的 MCU 参考手册。

## 12.3 使用 CubeMX 配置 ADC 外设

CubeMX 允许通过几个步骤轻松配置 ADC 外设。第一步是在 IP Tree 中启用所需的 ADC 通道，如图 12.11 所示。

![](img/9ef247bc7328ae96d37b38a68155_400.png)

> 图 12.11：IP Tree 允许选择 ADC 输入通道

一旦启用输入，我们就可以从 Configuration 配置 ADC 外设，如图 12.12 所示。

![](img/9ef247bc7328ae96d37b38a68155_400_1.png)

> 图 12.12：ADC 字段反映了此处看到的 ADC 参数。唯一让用户困惑的是通道配置方式。实际上，首先需要通过设置 `Number of Conversion` 字段来配置使用的通道数量。接下来（这非常重要），我们需要在配置对话框中为每个常规和注入组独立选择采样速度。CubeMX 将生成所有初始化代码。

如本章之前所述，`HAL_ADC` 模块与其他 HAL 不同。要启动软件驱动的转换，需要在 ADC 初始化期间指定参数 `hadc.ExternalTrigConv = ADC_SOFTWARE_START`。CubeMX 反映了此配置，但理解如何正确配置外设是复杂的。因此，为了启用软件驱动转换，`External Trigger Edge` 参数必须设置为上升沿。这会使 `External Trigger Source` 字段可用，你将需要选择 Software。

## 13. 数模转换

在上一章中，我们关注了 ADC 控制器，展示了所有 STM32 微控制器提供的该外设的相关特性。此操作的反向是数模转换（DAC）。取决于所使用的系列和封装，STM32 微控制器通常提供一个或两个输出的 DAC；除了 STM32F3 系列的 DAC 外，第一个有两个输出，另一个只有一个输出。某些 STM32G4 MCU 提供多达 5 个独立的 DAC 模块，但只有前两个具有输出：DAC 通道可以配置为 8/12 位模式工作，两个通道的转换可以独立执行或同步生成信号（例如音频应用中）。

### 13.1 DAC 简介

DAC 是一种将数字转换为模拟信号的设备，该信号与提供的电压 V_REF 成比例（见图 13.1）。DAC 有许多类别。其中包括脉宽调制器 (PWM)、插值、sigma-delta DAC 和高速 DAC。我们在第 11 章中分析了如何使用 STM32 生成 PWM 信号，并利用这种能力在 RC 低通滤波帮助生成了输出正弦波。

![](img/9ef247bc7328ae96d37b38a68155_402_0.png)

STM32 微控制器中的 DAC 外设基于常用的 R-2R 电阻网络。电阻阶梯是由重复电阻单元组成的电子电路，是使用高精度电阻制造的重复电阻网络进行数模转换的一种廉价且简单的方法。该网络作为参考电压和地之间的可编程分压器。

![](img/9ef247bc7328ae96d37b38a68155_403_0.png)

> 图 13.2：如何使用 R-2R 网络将数字量转换为模拟信号

图 13.2 显示了一个 8 位 R-2R 电阻阶梯网络。DAC 的每一位由数字逻辑门驱动。理想情况下，这些门将输入位在 V = 0（逻辑 0）和 V = V_{REF}（逻辑 1）之间进行切换。R-2R 网络导致这些数字位对输出电压 V_{OUT} 的贡献产生加权。取决于哪些位被设置为 1 哪些被设置为 0，输出电压将在 0 到 V_{REF} 减去对应 0 的最小步值之间产生相应的阶值。

对于具有 N 位和 0V/V_{REF} 逻辑电的 R-2R DAC 给数值 D，输出电压 V_{OUT} 为：

```
V_{OUT} = \frac{V_{REF} \times D}{2^N}
```

例如，如果 N = 12 (2^N = 4096) 且 V_{REF} = 3.3 V（STM32 微控制器的典型模拟电压），则 V_{OUT} 将在 0V（VAL = 00000000_2）和最大值（VAL = 4095 = 111111111111_2）之间变化：

```
V_{OUT} = 3.3 \times \frac{4095}{4096} \approx 3.29V
```

步进为（对应 VAL = 1）：

```
\Delta V_{OUT} = 3.3 \times \frac{1}{4096} \approx 0.0002V
```

然而，请始终记住，DAC 输出的精度和稳定性受 VDDA 电源域质量和 PCB 布局的严重影响。

在 STM32 微控制器中，DAC 模块具有 12 位精度，但它可以配置为以 8 位模式工作。在 12 位模式下，数据可以左对齐或右对齐。根据销售类型和所使用的封装，DAC 有两个输出通道，每个通道都有自己的转换器。在双 DAC 通道模式下，转换可以独立进行，也可以在两个通道分组在一起进行同步更新时同时进行。提供了一个输入参考电压 VREF+（与其他模拟外设共享）以获得更高的分辨率。与 ADC 外设一样，DAC 也可以与 DMA 控制器配合使用，以固定频率产生变变电压。这在音频应用中，或者当我们想要生成在给定载波频率工作的模拟信号时，非常有用。正如我们将在本章稍后部分看到的，STM32 DAC 具有生成噪声波和三角波的能力。

最后，在 STM32 MCU 中实现的 DAC 为每个通道集成了一个输出缓冲区（见图 13.2），该缓冲区用于降低输出阻抗并在无需添加外部放大器的情况下驱动外部负载。每个 DAC 通道的输出缓冲区都可以启用和禁用。

表 13.1 列出了我们书中考虑的配备九块 Nucleo 板的所有 STM32 MCU 的 DAC 外设确切数量及其相关的输出通道。

| Nucleo P/N | DAC 外设 | DAC 外部通道 |
|---|---|---|
| NUCLEO-G74RE | 4 | 3 |
| NUCLEO-F44RE | 1 | 2 |
| NUCLEO-F401RE | - | - |
| NUCLEO-F303RE | 1 | 2 |
| NUCLEO-F103RB | - | - |
| NUCLEO-F072RB | 1 | 2 |
| NUCLEO-L476RG | 1 | 2 |
| NUCLEO-L152RE | 1 | 2 |
| NUCLEO-L073RZ | 1 | 2 |

表 13.1：配备 Nucleo 板的 STM32 MCU 中 DAC 外设的可用性

### 13.2 HAL_DAC 模块

在简要介绍 STM32 微控制器中 DAC 外设提供的最重要的功能后，现在是深入研究相关的 CubeHAL API 了。

为了操作 DAC 外设，HAL 定义了 C 结构体 `DAC_HandleTypeDef`，其定义如下：

```c
typedef struct {
    DAC_TypeDef *Instance;                          /* 指向 DAC 描述符的指针 */
    DAC_TypeTypeDef State;               /* DAC 通信状态 */
    __IO HAL_DAC_StateTypeDef Lock;      /* DAC 锁对象 */
    HAL_LockTypeTypeDef
    DMA_HandleTypeDef *DMA_Handle1;  /* 通道 1 的 DMA 句柄指针 */
    DMA_HandleTypeDef *DMA_Handle2;  /* 通道 2 的 DMA 句柄指针 */
    __IO uint32_t ErrorCode;            /* DAC 错误代码 */
} DAC_HandleTypeDef;
```

让我们分析该结构体最重要的特性。

- `Instance`：指向我们要使用的 DAC 的指针。例如，`DAC` 是第一个 DAC 外设的描述符。
- `DMA_Handle[1,2]`：指向配置为在 DMA 模式下执行 D/A 转换的 DMA 句柄。在具有两个输出通道的 DAC 中，存在独立的 DMA 句柄用于为每个通道执行转换。

如所示，`DAC_HandleTypeDef` 结构体与目前使用的其他描述符不同。它没有用于 `HAL_DAC_Init()` 函数来配置 DAC 的专用 `Init` 参数。因为 DAC 的有效配置是在通道级进行的，并且需要 `DAC_ChannelConfTypeDef` 结构体，其定义如下：

```c
typedef struct {
    uint32_t DAC_Trigger;               /* 指定 DAC 通道的外部触发 */
    uint32_t DAC_OutputBuffer;          /* 指定是否启用 DAC 输出缓冲区 */
} DAC_ChannelConfTypeDef;
```

- `DAC_Trigger`：触发 DAC 转换的源。当使用 `HAL_DAC_SetValue()` 函数手动驱动 DAC 时，可以假设为 `DAC_TRIGGER_NONE`；当在 DMA 模式下驱动且没有时间“时钟”转换时，值为 `DAC_TRIGGER_SOFTWARE`；由专用定时器驱动转换的值为 `DAC_TRIGGER_Tx_TRGO`。
- `DAC_OutputBuffer`：启用输出缓冲区。

要配置 DAC 通道，我们使用函数：

```c
HAL_StatusTypeDef HAL_DAC_ConfigChannel(DAC_HandleTypeDef* hdac,
            DAC_ChannelConfTypeDef* sConfig, uint32_t Channel);
```

该函数接受 `DAC_HandleTypeDef` 结构体的实例指针、之前看到的 `DAC_ChannelConfTypeDef` 实例指针，以及用于配置第一个通道和第二个通道的宏 `DAC_CHANNEL_1` 和 `DAC_CHANNEL_2`。

在一些较近的 STM32 微控制器中，例如 STM32L476 或 STM32G474，DAC 提供了额外的低功率功能。例如，可以启用采样保持电路，在 DAC 断电时保持电压稳定。这对于电池供电的应用非常有用。在这些 MCU 中，`DAC_ChannelConfTypeDef` 的结构有所不同，允许配置这些额外功能。请参考你所考虑的 MCU 的 HAL 源代码。

### 13.2.1 手动驱动 DAC

DAC 外设可以手动驱动，也可以使用 DMA 和触发源（例如，专用定时器）。我们现在将分析第一种方法，适用于不需要高频转换的情况。

第一步是通过调用函数启动外设：

```c
HAL_StatusTypeDef HAL_DAC_Start(DAC_HandleTypeDef* hdac, uint32_t Channel);
```

该函数接受 `DAC_HandleTypeDef` 结构的实例指针，以及要激活的通道（`DAC_CHANNEL_1` 或 `DAC_CHANNEL_2`）。

一旦 DAC 通道启用，可以通过调用函数执行转换：

```c
HAL_StatusTypeDef HAL_DAC_SetValue(DAC_HandleTypeDef* hdac, uint32_t Channel,
uint32_t Alignment, uint32_t Data);
```

`Alignment` 参数可以是 `DAC_ALIGN_8R` 以 8 位模式驱动 DAC，`DAC_ALIGN_12B_L` 或 `DAC_ALIGN_12B_R` 分别以 12 位模式驱动 DAC。以下基于 Nucleo 的示例显示了如何手动驱动 DAC。

STM32 DAC 具有 12 位分辨率，我们必须使用以下公式将值 4095（对应最大输出电压）除以 200 阶：

```
$DACOutput = \left(\sin\left(x \cdot \frac{2\pi}{n_s}\right) + 1\right) \left(\frac{4096}{2}\right) [3]$
```

其中 $n_s$ 是样本数，在我们的示例中为 200。

使用上述公式，我们可以生成一个初始化向量，以 DMA 模式馈送 DAC。对于 ADC 外设，我们可以使用定时器按照 [2] 中给出的频率触发 TRGO 线。以下示例展示了如何在 STM32F02 MCU 中使用 DAC 生成 50Hz 正弦波。

```c
Filename: Core/Src/main-ex2.c

#define PI 3.14159

#define SAMPLES 200

/* Private variables */

DAC_HandleTypeDef hdac;

TIM_HandleTypeDef htim6;

DMA_HandleTypeDef hdma_dac_ch1;

/* Private function prototypes */

static void MX_DAC_Init(void);

static void MX_TIM6_Init(void);

int main(void) {

    uint16_t IV[SAMPLES], value;

    HAL_Init();

    Nucleo_BSP_Init();

    /* Initialize all configured peripherals */

    MX_TIM6_Init();

    MX_DAC_Init();

    for (uint16_t i = 0; i < SAMPLES; i++) {

        value = (uint16_t) rint(sin(((2*PI)/SAMPLES)*i+1)*2048);

        IV[i] = value < 4096 ? value : 4096;

    }

    HAL_DAC_Init(&hdac);

    HAL_TIM_Base_Start(&htim6);

    HAL_DAC_Start_DMA(&hdac, DAC_CHANNEL_1, (uint32_t)IV, SAMPLES, DAC_ALIGN_12B_R);

    while(1);

}
```

```c
40 41 /* DAC init function */

42 void MX_DAC_init(void) {

43 DAC_ChannelConfTypeDef sConfig;

44 GPIO_InitTypeDef GPIO_InitStruct;

45

46

47 _HAL_RCC_DAC1_CLK_ENABLE();

48

49 /**DAC Initialization */

50 hdac.Instance = DAC;

51 HAL_Init(&hdac);

52

53 /**DAC channel OUT config */

54 sConfig.DAC_Trigger = DAC_TRIGGER_T6_GO;

55 sConfig.OutputBuffer = DAC_OUTPUTBUFFER_ENABLE;

56 HAL_DAC_ConfigChannel(&hdac,&sConfig, DAC_CHANNEL_1);

57

58 /**DAC GPIO Configuration */

59 PA4

60      -----> DAC_OUT

61 GPIO_Struct.Pin = GPIO_PIN_4;

62 GPIO_Struct.Mode = GPIO_MODE_ANALOG;

63 GPIO_Struct.Pull = GPIO_NOPULL;
```
