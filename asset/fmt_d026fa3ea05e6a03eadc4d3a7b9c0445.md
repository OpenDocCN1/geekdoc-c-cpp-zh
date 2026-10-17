
data[1] = (uint8_t) (MemAddress & 0xFF);

/* 在临时缓冲区中拷贝 pData 数组的内容 */

memcpy(data+2, pData, len);

/* 我们现在准备好通过 I2C 总线传输缓冲区 */

returnValue = HAL_I2C_Transmit(hi2c, DevAddress, data, len + 2, HAL_MAX_DELAY);

if(returnValue != HAL_OK)
    return returnValue;

free(data);

/* 我们等待 EEPROM 有效地将数据存储在内存中 */

while(HAL_I2C_Transmit(hi2c, DevAddress, 0, 0, HAL_MAX_DELAY) != HAL_OK);

return HAL_OK;

```

现在我们可以关注使用 EEPROM 的两个例程。它们都被设计为接受：
- EEPROM 的 I2C 地址 (`DevAddress`);
- 读取数据的内存地址 (`MemAddress`);
- 用于与 EEPROM 交换数据的内存指针 (`pData`);
- 要存储/读取的数据量 (`len`);

`Read_From_24Cxx()` 计算内存地址的两部分（MSB 和 LSB）。然后它通过 `HAL_I2C_Transmit()` 例程发送这两个部分。正如所述，24Cxx 内存的设计是设置内部计数器。我们可以在内存中启动一个新的事务来从 EEPROM 获取数据。

`Write_To_24Cxx()` 执行了类似的操作，但方式不同。它必须遵循图 14.9 所示的 24Cxx 协议。这意味着我们使用两个事务处理内存地址和数据，但必须执行唯一的事务。因此，我们使用了一个临时缓冲区（第 90 行），包含了内存地址以及要存储的数据。我们可以在 I2C 总线上执行传输（第 98 行），然后等待 EEPROM 完成传输（第 107 行）。

### 14.2.1 I/O 操作

2Cxx EEPROM 使用的协议适用于具有内存寻址寄存器的所有 I2C 设备。例如，HTS21 等 I2C 传感器采用了相同的协议。因此，ST 工程师已经在 CubeHAL 内部实现了更好、更快的 `Read_From_24LCxx()` 和 `Write_To_24LCxx()`：

```c
HAL_StatusTypeDef HAL_I2C_Mem_Write(I2C_HandleTypeDef *hi2c, uint16_t DevAddress, uint16_t MemAddress, uint16_t MemAddSize, uint8_t *pData, uint16_t Size, uint32_t Timeout);

HAL_StatusTypeDef HAL_I2C_Mem_Read(I2C_HandleTypeDef *hi2c, uint16_t DevAddress, uint16_t MemAddress, uint16_t MemAddSize, uint8_t *pData, uint16_t Size, uint32_t Timeout);
```

允许从内存寻址的 I2C 设备检索数据，但有一个显著区别：`HAL_I2C_Mem_Write()` 函数并没有像我们在上一个示例第 107 行那样按写入周期设计。但即使对于这种操作，HAL 提供了一个专用的、更移植的例程：

```c
HAL_StatusTypeDef HAL_I2C_IsReady(I2C_HandleTypeDef *hi2c, uint16_t DevAddress, uint32_t Trials, uint32_t Timeout);
```

该函数在返回错误之前最多接受 `Trials` 次尝试，但如果我们将 `HAL_MAX_DELAY` 传递给函数作为 Timeout，就可以向 Trials 参数传递 1。当轮询的 I2C 设备就绪时，函数返回 `HAL_OK`。否则，它返回 `HAL_BUSY`。

因此，`main()` 函数可以重排如下：

```c
int main(void) {

    char wmsg[]="we love STM32!";

    char rmsg[20];

    HAL_Init();

    Nucleo_BSP_Init();

    MX_I2C1_Init();

    HAL_I2C_Mem_Write(&hi2c, 0xA0, 0xAA, I2C_MEMADD_SIZE_16BIT, (uint8_t*)wmsg, strlen(wmsg)+1, HAL_MAX_DELAY);

    while(HAL_I2C_IsReady(&hi2c, 0xA0, 1, HAL_MAX_DELAY) == HAL_OK);

    HAL_I2C_Mem_Read(&hi2c, 0xA0, 0xAA, I2C_MEMADD_SIZE_16BIT, (uint8_t*)rmsg, strlen(rmsg)+1, HAL_MAX_DELAY);

    if(strcmp(wmsg, rmsg) == 0) {

        while(1) {

            HAL_GPIO_TogglePin(LD2_GPIO_Port, LD2_Pin);

            HAL_Delay(100);

        }

    }

    while(1);

}
```

上述 API 在轮询模式下工作，但 CubeHAL 也提供了相应的例程在中断和 DMA 模式下执行事务。按照惯例，这些其他 API 具有相似的函数签名，只需注意一点：用于信号传输结束的回调函数是 `HAL_I2C_MemTxCCallback()` 和 `HAL_I2C_MemRxCCallback()`，如表 14.3 所示。

### 14.2.1.2 嵌入式事务

24LCxx EEPROM 的读操作传输序列是一个事务。在反转总方向（从写到读）之前使用了重启条件。在第一个示例中，我们在 `Read_From_24LCxx()` 中使用了两个分离的事务。24Cxx EEPROM 的工作方式相同。可以注意到内部地址计数器设置了地址；第二个（读模式下执行）从 EEPROM 获取数据。然而，这并没有减少可以达到的最大吞吐量，反而会导致代码不可移植性：存在某些 I2C 设备严格遵守 I2C 协议，并使用重启条件来实现组合事务（因此它们在中间不允许停止条件）。

CubeHAL 提供了两个专用的例程来处理组合事务，或者在 Cube HAL 中被称为顺序事务：

```c
HAL_I2C_Master_Sequential_Transmit_IT(I2CHandTypeDef *hi2c, uint16_t *pData, uint16_t Size, uint32_t XferOptions);

HAL_I2C_Master_Receive_IT(I2CHandTypeDef *hi2c, uint8_t *pData, uint16_t Size, uint32_t XferOptions);
```

与其他 API 相比，这里唯一需要强调的参数是 `XferOptions`。可以假设它是表 14.4 所示的值之一，并用于驱动单次事务中启动/重启/停止 的生成。两个函数都以这种方式工作。假设我们需要从 24LCxx EEPROM 读取 n 字节。根据 I2C 协议，我们必须执行以下操作（参考图 14.10）：

- 1. 我们必须以写模式开始一个新事务，发送启动条件，随后是从机地址；
- 2. 我们传输两个包含内存地址高位和低位部分的字节；
- 3. 我们发送重启条件并传输从机设备地址，将最后一位设置为 1 以表示读事务。
- 4. 从机开始逐字节地发送数据，直到我们通过发送 NACK 或停止条件来结束事务。

### 表 14.4：用于驱动 STAR/RESTART/STOP 条件生成的 XferOptions 参数值

| 传输选项 | 描述 |
|---|---|
| I2C_FIRST_FRAME | 此选项允许仅生成 START 条件，而不在传输结束时生成最终的 STOP 条件。当传输方向发生变化时（如此），此选项允许在传输数据之前生成 RESTART 条件。 |
| I2C_NEXT_FRAME | 在 `HAL_I2C_Master_Sequential_Receive_IT()` 之后调用 `HAL_I2C_Master_Sequential_Transmit_IT()`（或反之），或者在方向没有发生变化的情况下，允许仅管理新数据的传输，且两种情况下均**不**生成最终 STOP 条件。当传输方向发生变化时（如此），此选项允许在传输数据之前生成 RESTART 条件；`HAL_I2C_Master_Sequential_Transmit_IT()` 之后调用 `HAL_I2C_Master_Sequential_Receive_IT()`（或反之），或者在方向没有发生变化的情况下，允许仅管理新数据的传输，且两种情况下均**会**生成最终 STOP 条件。 |
| I2C_FIRST_AND_LAST_FRAME | 无顺序使用：该例程的工作方式与 `HAL_I2C_Master_Sequential_Transmit_IT()` 和 `HAL_I2C_Master_Sequential_Receive_IT()` 函数相同。 |

通过*顺序传输*，我们可以按照以下方式进行：

- 1. 我们通过传递从机地址和内存位置地址调用 `HAL_I2C_Master_Sequential_Transmit_IT()` 例程；通过传递值 `I2C_FIRST_FRAME`，以便它生成一个 START 条件，且在发送两个字节后不发出 STOP 条件；
- 2. 我们调用所有的 `HAL_I2C_Master_Sequential_Receive_IT()` 例程，通过传递从机地址、用于读取字节的缓冲区指针、从 EEPROM 读取的字节数以及值 `I2C_LAST_FRAME`，以便该函数生成一个 RESTART 条件并在结束时通过发出 STOP 条件来终止。

### 14.2.1.3 关于 STM32F0/L0/L4 家族时钟配置的说明

在 STM32F0/L0 家族中，可以为 I2C1 外设选择不同的时钟源。这是因为在这些家族中，I2C 外设即使在低功耗模式下工作，当在从机模式工作且配置的从机地址位于总线上时，会唤醒 MCU。更多信息请参考 CubeMX 中的 *Clock view*（时钟视图）。

在 STM32L4/5 MCU 中，可以为所有 I2C 外设选择时钟源。

## 14.2. 在从机模式使用 I2C 外设

如今市场上有很多板级系统（SoB）模块。这些通常是已经集成了若干 IC 的小型 PCB，专门用于执行某些相关任务。GPRS 和 GPS 模块或多传感器板都是 SoB 模块的示例。这些模块随后焊接在主板上，得益于它们侧面暴露了焊接焊盘，称为“阶梯孔”（castellated vias 或 castellations）。**图 14.11** 显示了 ST 的 STEVAL-STLCS01V1¹⁴ 传感器开发套件，这是一个集成且可编程的模块，带有 STM32L476、三个高度集成传感器（6 轴数字电子罗盘和 3 轴数字陀螺仪、气压计、麦克风）以及蓝牙低功耗（BLE）网络处理器 BlueNRG-MS。

![](img/9ef247bc7328ae96d937b3818a681558_436_0.png)

图 14.11：ST 的 STEVAL-STLCS01V1 传感器开发套件

这些板上的 MCU 通常预先程序了固件，该固件专门用于执行某项任务。主板还包含另一个可编程的 IC 或类似的 MCU。主板使用常用的通信协议与 SoB 交互，通常为 UART、CAN 总线、SPI 或 I2C 总线。由于这些原因，经常需要对 STM32 设备进行 FC编程。

CubeHAL 提供了开发从机应用程序所需的全部胶接代码。从机例程与用于主模式编程的外设的例程相同。例如，以下例程用于在外设处于从机模式时传输/接收数据：

```c
HAL_StatusTypeDef HAL_I2C_Slave_Transmit_IT(hi2c, uint8_t *pData,
                                            uint16_t Size);

HAL_StatusTypeDef HAL_I2C_Slave_Receive_IT(hi2c, uint8_t *pData,
                                            uint16_t Size);
```

同样，在数据传输/接收结束时调用的回调如下：

```c
void HAL_I2C_SlaveTxCpltCallback(I2CHandle *hi2c);

void HAL_I2C_SlaveRxCpltCallback(I2CHandle *hi2c);
```

我们现在获得了一个完整的示例，展示了如何使用 CubeHAL 开发从机应用程序。我们将实现一种类似于市场上大多数数字温度传感器的数字温度传感器（例如流行的 TI 的 TMP275 和 ST 的 HT221）。这个“传感器”提供三个寄存器：

- 一个 WHO_AM_I 寄存器，用于主代码检查 I2C 接口是否工作正常；该寄存器返回固定值 0BC。
- 两个温度相关的寄存器，命名为 TEMP_OUT_INT 和 TEMP_OUT_FRAC，包含采集温度的整数部分和小数部分；例如，如果检测到的温度等于 27.34°C，那么 TEMP_OUT_INT 寄存器包含值 27，TEMP_OUT_FRAC 包含值 34。

![](img/9ef247bc7328ae96d937b3818a681558_437_0.png)

我们的传感器将被设计为响应一种基于组合事务的非常简单的协议，如图 14.12 所示。如你所见，与 24ICxx 在随机模式访问内存时使用的协议相比，唯一的区别在于主寄存器的大小，在这种情况下仅为一个字节。

```c
i2cBuf[0] = t_int;

break;

case TEMP_OUT_FRAC_REGISTER:

i2cBuf[0] = t_frac;

break;

default:

i2cBuf[0] = 0xFF;

}
```

```c
HAL_I2C_Slave_Sequential_Transmit_IT(&h12c, I2cBuf, 1, I12C_LAST_FRAME);

while (HAL_I2C_GetState(&h12c) != HAL_I2C_STATE_READY)

}
```

`main()` 函数最相关的部分从第 46 行开始。`HAL_I2C_EnableListen_IT()` 程序开启了所有与 I2C 外设相关的中断。这意味着当主设备放置从设备地址（由主设备 `I12C_SLAVE_ADDR` 定义）时，将触发一个新中断。`HAL_I2C_EV_IRQHandler()` 程将会自动调用我们将分析的 `HAL_I2C_AddrCallback()` 函数。

`main()` 函数随后每秒对内部温度传感器进行一次 A/D 转换，并将获取的温度（存储在 `temp` 变量中）分为 8 位整数 `t_int` 和 `t_frac`：这些代表温度的整数部分和小数部分。当 `requestedVariable` 等于 1 时，`main` 函数停止 A/D 转换：该全局变量由 `HAL_I2C_AddrCallback()` 函数根据 `transferDirection` 设置，该变量包含了 I2C 事务的传输方向（读/写）。

如果主设备正在以写模式启动一个新事务，则意味着它正在传输寄存器地址。在第 72 行调用了 `HAL_I2C_Slave_Sequential_Receive_IT()`：这将导致从主设备接收寄存器地址。由于该函数在中断模式下工作，我们需要一种方法等待传输完成。`HAL_I2C_GetState()` 返回 HAL 的内部状态，该状态等于 `HAL_I2C_BUSY_RX_LIST`，我们可以通过向主设备传输等待器的内容继续操作。

这一操作在第 89 行完成，此时调用了函数 `HAL_I2C_Slave_Sequential_Transmit_IT()`：该函数插入传输方向，并向主设备发送等待器的内容。棘手部分在第 90 行解决。在这里，我们等待 I2C 传输状态等于 `HAL_I2C_STATE_READY`。为什么我们不像第 737 行所做的那样一直检查外设状态直到 `HAL_I2C_STATE_LIST` 状态呢？为了理解这一点，我们需要记住使用组合事务时的一项重要事项。当一个事务触发传输方向时，主设备会开始对每个字节进行应。记住，只有主设备知道事务持续多久，并由它决定停止事务。在组合事务中，主设备通过发送 NACK 来结束从从设备到主设备的传输，这会导致从设备发出 STOP 条件。从 I2C 外设的角度来看，STOP 条件会导致外设退出监听模式（从技术上说，它产生了一个中止条件 - 如果你实现了 `HAL_I2C_AbortCpltCallback()`，*注：此处你可以跟踪这种情况何时发生*），这就是为什么我们需要检查是否等于 `HAL_I2C_STATE_READY` 状态并在第 46 行将外设置于监听模式的原因。

文件名：src/main-ex2.c

```c
#else // Master board

i2cBuf[0] = WHO_AM_I_REGISTER;

HAL_I2C_Master_Sequential_Transmit(&hi2c1, I2C_SLAVE_ADDR, i2cBuf,
                               1, I2C_FIRST_FRAME);

while (HAL_I2C_GetState(&hi2c1) != HAL_I2C_STATE_READY);

HAL_I2C_Master_Sequential_Receive(&hi2c1, I2C_SLAVE_ADDR, i2cBuf,
                               1, I2C_LAST_FRAME);
```
