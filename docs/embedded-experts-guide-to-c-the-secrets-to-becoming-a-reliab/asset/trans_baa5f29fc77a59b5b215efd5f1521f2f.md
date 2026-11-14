

嘈杂的数字输入，其中电磁干扰可能导致状态短暂、虚假的变化。

```c
/* Debounce a switch by checking
 * for five consecutive 'true' inputs. */
bool debounce(bool state)
{
    static int sample_count = 0U;
    static bool debounced_state = true;
    /* If it's time to restart sampling, reset the

    * state variables. */
    if (!(debounced_state || (5U == sample_count)))
    {
        debounced_state = true;
        sample_count = 0;
    }
    /* AND the current state with the stored
     * state, then increment the number of
     * samples. */
    debounced_state &= state;
    ++sample_count;
    /* Return true after five true inputs. */
    return debounced_state &&
        (5U == sample_count);
}
```

图 5.3 - 开关可以定期采样并在软件中进行消抖。此示例展示了一个简单函数，每次采样开关时都可以调用该函数，并在连续五个“真”输入后返回“真”。

与输入类似，输出可以定期更新或仅在需要时更新，适当的选择在很大程度上取决于其用途。大多数输出将是数字输出；要么是单个信号（可能是开或关），要么是多个输出，通常被称为可以承载二进制的输出。然而，情况并非总是如此，许多平台还包括模拟输出。

简单输出可以包括 LED、蜂鸣器、电磁阀和这些设备，这些都可以使用单个输出进行控制，将其打开和关闭；虽然也可以通过在开和关状态之间快速切换来改变 LED 强度或电机速度等属性，每个状态的相对时间决定输出——这种技术称为脉冲宽度调制。对于需要有限带宽的输出，无需任何专用硬件即可实现这一点，尽管 PWM 模块是现代微控制器的常见功能。可以通过使用更高开关频率的 PWM 或使用专用数模转换器 (DAC) 来实现更精确的模拟输出。

```c
/* Generate simple PWM signals. The bandwidth
 * of the input must be much less than the
 * frequency at which the compare signal
 * wraps-around. */
bool pwm(uint8_t input)
{
 static uint8_t counter = 0U;
 /* Increment counter. The value wraps back to
 * zero when it exceeds 255. */
 ++counter;
 /* Return true when the input exceeds the
 * counter value. */
return (input >= counter);
}
```

图 5.4 - 低频 PWM 可以使用计数器并将值与调制信号进行比较来实现。这种方法适用于仅需要约 100 Hz 调制频率的指示 LED 等输出，但更好的性能需要硬件支持。调制信号的带宽必须低于载波信号（低五倍或更多）。载波信号频率是函数被调用的频率除以计数器回绕前的增量次数。

## 总线

总线是外设和设备之间传输数据的物理手段。这是一个广义术语，涵盖用于互连的硬件和协议，这些互连可以是并行或串行，也可以是同步或

并行总线是使用单独的物理连接同时传输多个位的总线；反之，串行总线一次使用一个物理连接传输一个位。并行总线的带宽可以通过简单增加连接数量来提高，从而允许一次传输更多位。从历史上看，这曾被视为一种优势，当低成本而非高性能是重要要求时，会使用串行通信；然而，对于高速总线，匹配每个互连的电气特性是一项重大挑战，因此除专用应用外，通常更倾向于串行总线。同步总线是指设备还共享时钟信号以控制数据传输时序的总线，而异步总线则通过其他方式控制时序。许多常见总线，例如 Ethernet 和 USB 都是异步串行总线；虽然今天它们对普通最终用户来说不那么熟悉，但 RS232 和 RS485 也是异步串行总线，并且仍在许多嵌入式系统中使用。同步串行总线，例如 SPI 和 I2C，通常在设备内部发现。并行总线现在比过去少得多，至少在实现通用通信方面是如此。

大多数总线至少在理论上可以使用一种称为位操作的技术来实现——即使用软件来模拟专用硬件的行为。虽然这偶尔可能是必要的，但它通常效率低下、麻烦，并且在除最低数据速率外的任何情况下都完全不切实际，尤其是在与串行协议一起使用时。此外，协议的某些要求在软件中可能难以甚至不可能模拟；例如，数据可能需要在时钟信号的上升沿写入并在下降沿读取（或反之），这在硬件中（至少在理论上）很容易实现，但在软件中则不然。由于包含至少一个通用异步收发发射器、SPI 或 I2C 模块的廉价微控制器很常见，使用这些协议进行通信的各种外设也很常见，因此在几乎所有情况下都应优先使用专用硬件。

```c
/* The bus itself is defined somewhere else. */
extern spi_bus_t g_spi;
/* Send and receive one byte of data using an
 * SPI bus at the maximum possible data
 * rate. */
uint8_t spi_transceive(uint8_t data_in, uint8_t device)
{
    uint8_t data_out = 0U;
    /* Set the device address pins to the selected
     * device. Device selects are active low. */
    g_spi.n_cs = ~device;
    /* Send and receive data bit-by-bit. To lower
     * the data rate, add delays. */
    for (bit = 0U; 8U > bit; ++bit)
    {
        /* Write one bit, set clock high. */
        g_spi.mosi = data_in & 0x80U;
        g_spi.clk = 1U;
        /* Shift input and output bits to the
         * right. */
        data_in <<= 1;
        data_out <<= 1;
        /* Set clock low, read one bit. */
        g_spi.clk = 0U;
        data_out |= g_spi.miso;
    }
    /* Set all device address pins high to
     * deselect. */
    g_spi.n_cs = 0xFFU;
    /* Return the data read from the device. */
    return data_out;
}
```

图 5.5 - 位操作是在软件中满足总线要求并直接读写位而不是通过硬件的一种技术。此示例展示了如何为 SPI 总线实现此功能。位操作确实存在一些挑战。例如，请注意，该示例不努力精确控制总线时序；可以使用定时器中断或在语句之间插入“NOP”（无操作）指令来解决此问题，但专用硬件完全避免了这种需求，并且在可用时应始终是首选方案。

总线上的单个设备可以在软件中使用包含与其通信所需信息的字段的结构来表示；这包括标识信息、发送和接收缓冲区以及在接收数据或发生错误时调用的回调函数。这些结构应仅对相关设备和总线驱动程序模块可见，并且应仅在应用程序代码中使用指针间接引用。这样的指针可能被称为设备句柄。这样做有两个很好的理由。

- 首先，它在设备的实现与应用程序与其交互的方式之间提供了一定程度的抽象，这既简化了应用程序的开发，也使它们更具可移植性。

- 其次，它防止程序员意外或天真地更改实现。

