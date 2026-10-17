
pdata[0] = NACK;

HAL_UART_Transmit(UART2, pdata, 1, HAL_MAX_DELAY);

}

}

# 启动过程

上面的代码展示了命令的实现。如你所示，CRC 是从 UART 接收的消息中提取的，并与 CRC 外设计算出的 CRC 进行比较。请注意，CRC 外设具有 32 位宽的数据寄存器，且 CRC-32 是对整个寄存器计算的，我们将前两个字节转换为 32 位值。

如果 CRC 匹配，则会填充 `FLASH_EraseInitStruct` 结构体的实例，以便从第二个扇区（第 193 行）擦除到指定的扇区数量（第 194 行）。闪存存储器将被解锁（第 198 行），并通过调用 `HAL_FLASH_Erase()` 例程执行擦除程序。

# 写入命令

`CMD_WRITE` 命令用于从内存位置开始存储 16 字节（即 4 个字），其结构如图 22.7 所示。该命令由两部分组成。第一部分由命令 `0xb` 计算，随后是放置数据字节的起始地址和 CRC-32。如果 CRC 匹配且指定地址大于或等于 `APP_START_ADDRESS`，引导加载程序将用 ACK 回复。引导加载程序期望接收另一个 16 字节序列以及这些字节的 CRC-32 校验和。

| 1 字节 | 4 字节 | 4 字节 |
| :--- | :--- | :--- |
| 0x2b | 内存地址 | CRC-32 |
| | 16 字节 | 4 字节 |
| 数据 | ... | 数据 CRC-32 |

图 22.7：CMD_WRITE 的结构

```c
Filename: src/main-bootloader.c

void cmdWrite(uint8_t *pData) {

    uint32_t ulSaddr = 0, ulCRC = 0;

    memcpy(&ulSaddr, pData + 1, sizeof(uint32_t));

    memcpy(&ulCRC, pData + 5, sizeof(uint32_t));

    uint32_t pData[5];

    for (int i = 0; i < 5; i++)

        pData[i] = pData[i];

    /* 检查提供的 CRC 是否正确 */

    if (ulCRC == HAL_FLASH_Calculate(&crc, pData, 5) && ulSaddr >= APP_START_ADDRESS) {
```

```c
279    /* 发送 ACK */

280    pucData[0] = ACK;

281    HAL_UART_Transmit(&huart2, (uint8_t *) pucData, 1, HAL_MAX_DELAY);

282

283    /* 现在获取给定的字节数加上 CRC32 */

284    if (HAL_UART_Receive(&huart2, pucData, 16 + 4, 200) == HAL_TIMEOUT)

285        return;

286
```

```c
287    memcpy(&uLrc, pucData + 16, sizeof(uint32_t));

288

289    /* 检查 CRC 是否正确 */

290    if (uLrc == HAL_CRC_Calculate(&hCrc, (uint32_t*) pucData, 4)) {

291        HAL_Flash_Unlock();//解锁闪存存储器

292

293        /* 解码发送的字节，使用 AES-128 ECB */

294        aes_enc_dec((uint8_t*) pucData, AES_KEY, 1);

295        for (uint8_t i = 0; i < 16; i++) {

296

297            /* 从指定的地址将每个字节存储到闪存存储器 */

298            HAL_Flash_Program(FLASH_TYPEPROGRAM_BYTE, uSaddr, pucData[i]);

299            uSaddr += 1;

300        }

301        HAL_Flash_Lock();//锁定闪存存储器
```

```c
302    /* 发送 ACK */

303    pucData[0] = ACK;

304    HAL_UART_Transmit(&huart2, (uint8_t *) pucData, 1, HAL_MAX_DELAY);

305    } else {

306        goto sendack;

307    }

308    } else {

309        goto sendack;

310    }
```

```c
312    sendack:

313    pucData[0] = NACK;

314    HAL_UART_Transmit(&huart2, (uint8_t *) pucData, 1, HAL_MAX_DELAY);

315}
```

上面的代码展示了该命令的实现。如你所示，CRC 是从 UART 接收的消息中提取的，并与 CRC 外设计算出的 CRC 进行比较。如果 CRC 匹配且指定地址大于或等于 `APP_START_ADDRESS`，引导加载程序将用 ACK 回复。引导加载程序期望接收另一个 16 字节序列以及这些字节的 CRC-32 校验和。如果这些其他字节的 CRC-32 匹配（第 290 行），发送的数据字节将使用 AES-128 算法和预共享密钥解密。

> `aes_enc_dec()` 函数是由 Eric Peeters 编写的一个库，它可以从 TI 网站 (https://www.ti.com/tool/AES-128) 下载，并且其许可证允许自由使用。

ST 为 STM32 平台提供了一个完整的加密库，该库与 Cube 框架 (https://bit.ly/2zWN) 兼容。该库也适用于具有专用硬件单元的 MCU。然而，该库的许可证阻止作者在示例中发布该库。

在闪存存储器中还有一个函数需要分析：由 `main()` 函数调用的 `CHECK_AND_FLASH_PROTECTION()` 将 `ENABLE_BOOTLOAD_PROTECTION` 设置为 1。

```c
Filename: src/main-bootloader.c

void CHECK_AND_FLASH_PROTECTION(void) {

    FLASH_OBInitTypeDef ob;

    /* 获取 OB */

    HAL_FLASH_OBConfig(&ob);

    /* 如果第一个扇区未保护 */

    if ((ob.WRPConfig & OB_WRP_SECTOR_0) != OB_WRP_SECTOR_0) {

        HAL_FLASH_Unlock();//解锁闪存

        HAL_OB_Unlock();//解锁 OB

        ob.OptionType = OPTIONTYPE_WRP;

        ob.WRPState = OB_WRP_STATE_ENABLE;//启用 WRP 写入

        ob.WRPConfig = OB_WRP_SECTOR_0;//开启第一个扇区的 WRP

        HAL_FLASH_OBProgram(&ob); //写入 OB

        HAL_FLASH_OBLaunch(); //确保新配置保存到闪存中

        HAL_OB_Lock //锁定 OB

        HAL_FLASH_Lock //锁定闪存

    }

}
```

此函数简单地获取当前的 Option Bytes 并检查第一个扇区是否受写保护（第 324 行）。如果没有，则启用写保护，以防引导加载程序被覆盖。如果你想尝试此函数，可以使用 STM32CubeProgrammer 写保护。

# 对自定义引导加载程序的考虑

这里介绍的自定义引导加载程序远不完整。它缺少一些功能，而且在处理错误情况方面并不健壮。此外，对于 STM32F0 平台的引导加载程序在使用 `-Os` 编译时约为 3KB，这对于引导加载程序来说太大了。遗憾的是，HAL 对最终二进制镜像的大小有不可忽视的开销。设计良好的引导加载程序会尽可能减小内存占用。这一方面不在本书的范围内，本书仅展示了启动过程背后的基本概念。

## 2.3.1 STM32F0 微控制器中的向量表重定向

因此，我们已经看到在基于 Cortex-M0 的微控制器中无法像 Cortex-M0+/3/4 MCU 那样重定向向量表。这意味着我们不能使用之前的代码（第 154-161 行）将控制权交给主固件，因为 Cortex-M0 核心总是在地址 `0x00000000` 找到向量表，这与我们场景中引导加载程序的向量表重合。

然而，我们可以用更巧妙的方法绕过这个限制。我们将分析的想法基于内存映射允许 `0x20000000` 处的 SRAM 内存，而原始闪存可以通过 `0x08000000` 访问。我们可以在控制权交给 SRAM 内部的“目标”表并执行物理映射之前，重定向主固件的向量表。目标表中包含的地址仍然可以在其原始位置访问，允许异常处理程序和 ISR 正确执行。

图 22.8 尝试表示这一过程。在左侧是主应用程序（未显示引导加载程序）。为了简单起见，假设其向量表放置在地址 `0x08002C00`。这意味着从地址 `0x08002C00` 开始，我们拥有内存中 Cortex-M0 异常处理程序和 ISR 的地址。显然，如图 22.8 中灰色箭头所示，这些地址指向闪存内存。

![img/9ef24bc732ae96d37b381a65580.png](img/9ef24bc732ae96d37b381a65580.png)

图 22.8：向量表在 STM32F0 微控制器中的重定向

引导加载程序按以下方式运行。它将向量表复制到 SRAM 中，从初始地址 `0x20000000` 开始。这意味着 `0x00000000` 地址指向闪存内存。在复制完成后，内存被重映射，使得 `0x00000000` 地址现在与 SRAM 内存重合。控制权转移到主固件的异常处理程序及其执行位置。

# 启动过程

我们感兴趣的代码从第 155 行开始。定义了两个指针：一个指向 SRAM 的开头（`pulSRAMbase`），另一个指向主固件的开头（`pulFlashBase`），根据上一个示例，该值等于 `0x00002C00`。[158:162] 处的循环对 SRAM 中的向量表进行拷贝，直到当前闪存器内存位置包含值 `0xAABBCCD`（更多信息请参阅[此处](#)）。随后，将 MSP 设置为 SRAM 的末尾（这通常是不必要的，只是以防万一……），并执行物理复位（第 167 行）。最后将控制权转移到主固件。

有几点需要注意。首先，为了简化拷贝过程并避免向量表被不断增长的栈覆盖，向量表是从其起始位置拷贝到 SRAM 的，其余的应用程序数据（由 `.data` 节、`.bss`、堆和栈组成）则紧随其后放置（见图 22.8）。这要求主固件的链接器脚本经过正确配置，如下所示：

```
MEMORY

FLASH (rx) : ORIGIN = 0x00002C00, LENGTH = 64K - 10K

RAM (xrw) : ORIGIN = 0x20000B00, LENGTH = 8K - 0xB8
```

其次，我们需要知道向量表何时结束。应用程序中通常不会启用所有的中断请求（IRQ），我们可以将哨值 `0xAABBCCD` 放在紧跟最后一个使用的 IRQ 之后的第一个条目。例如，假设我们的固件在中断模式下使用 USART2，可以看到该 IRQ 是向量表中的第 46 个条目。我们可以将该值放在第 47 个位置。通过修改 `startup_stm32f0xx.s` 文件可以轻松实现，如下：

```
Filename: src/startup_stm32f030.s

180 .word SPI1_IRQHandler      /* SPI1 */      /

181 .word SPI2_IRQHandler      /* SPI2 */      /

182 .word USART1_IRQHandler  /* USART1 */     /

183 .word USART2_IRQHandler  /* USART2 */     /

184 .word 0xAABBCCD         /* Reserved */    /

185 .word                   /* Reserved */    /

186 .word 0                  /* Reserved */    /
```

通过这种方式，我们有了一种通用且方便的方法来设置向量表的结束。查看之前的链接器脚本片段，从 SRAM 内存大小中减去值 `0xB`（十进制为 184）。将 184 除以 4 字节，得到 46，这对应于最后一个向量表条目。

最后，请注意 SYSCFG 是一个独立于 Cortex-M 核心的外设，我们需要通过调用 `_HAL_RCC_SYSCFG_CLK_ENABLE()` 来启用它。

# 22.3 如何使用 flasher.py 工具

如所述，你可以在本章节的图书源文件中找到一个名为 `flasher.py` 的 Python 脚本。该工具允许将使用 Intel HEX 二进制格式生成的 MCU 固件上传到 MCU 中。该格式是 Intel 几年前开发的一种二进制文件规范，目前在低成本嵌入式平台中仍然广泛使用。该脚本的源代码未在此显示，但很容易理解为什么要制作它。该脚本需要三个额外的模块：`pyserial`、`IntelHex` 和 `pycryptodome` 库。

你可以使用 `pip` 命令轻松安装它们：

```
$ sudo pip install intelhex pycryptodome pyserial
```

该脚本设计为在命令行接受两个参数：

- 对应 Nucleo VCP 的串口
  - 在 Windows 中，这等同于 'COMx' 字符串，“x" 必须替换为数字。
  - 在 Linux 或 Mac 中，这对应于 /dev/tty（通常是 /dev/ttyACM0 或类似名称）。

![img/9ef247bc0328ae96d3b18a681558_611.png](img/9ef247bc0328ae96d3b18a681558_611.png)
图 22：HEX 格式的二进制文件

默认情况下，GNU 工具链会自动生成编译后的固件 HEX 文件。你可以在 build 文件夹中找到它：

> `pycryptodome` 是一个哈希函数集合（如 SHA256 和 RIPD160），以及各种加密算法（如 AES, RSA）的库。`intelhex` 是一个可以方便操作 Intel 文件的小型库，由 Alexander Belchenko 开发并根据 BSD 协议发布。

![img/9ef247bc0328ae96d3b18a681558_612.png](img/9ef247bc0328ae96d3b18a681558_612.png)
图 22.10：如何获取 HEX 文件的路径

你可以通过右键点击它并选择属性来获取完整路径，如 22.10 所示。

# 运行 FreeRTOS

实时操作系统（RTOS）利用 Cortex-M 核心提供的计算能力，引入了线程¹的概念，即一种与其他线程竞争 MCU 资源的独立执行流。此外，由于物联网（IoT）的日益普及，许多 RTOS 通过增加连接解决方案和云平台进行了演进。由于 Cortex-M 是许多芯片制造商的标准架构，STM32 开发者可以根据对复杂性处理的需求从多种 RTOS 中进行选择。

传统上，ST 电子支持一种非常流行且免费的 RTOS：FreeRTOS。FreeRTOS 已成为电子行业的一种标准，并被开源社区广泛采用。根据某些统计数据²，目前的 CubeMX 版本为所有 STM32 微控制器提供了 FreeRTOS 10.x 的完整集成。FreeRTOS 在 2017 年被亚马逊收购，现在是 AWS 生态系统的一部分。它根据更宽松且“对商业友好”的 MIT 协议发布。

> ¹ 线程：一种与其他线程竞争 MCU 资源的独立执行流。
> ² https://bit.ly/3mX3QTE0

## 运行 FreeRTOS

在近年来，FreeRTOS 的进化主要集中在 AWS IoT 服务的集成上。

然而，ST 在 2020 年 12 月宣布与微软达成关键合作，微软最近收购了 ThreadX RTOS 背后的公司，并将其更名为 Azure RTOS。微软正在全力开发嵌入式平台的完整 IoT 解决方案生态系统，而 Azure RTOS 是微软提供的核心元素。这种合作是互利的：ST 将 Azure RTOS 作为 STM32Cube 扩展包进行集成，而微软将推动 STM32 微控制器作为 IoT 应用程序的参考“平台”。ST 对 RTOS 的支持不仅限于内核。该集成将包括：FileX（一种在 NAND 和 NOR 闪存上提供高级功能，如容错或磨损均衡的的文件系统）；NetX 和 NetX Duo（基于 TCP/IP、IPv4 和 IPv6 的网络栈，以及 IoT 中使用的如 MQTT 或 COAP 等许多上层协议）；USBX（利用 USB 接口，既作为主机也作为设备，并拥有一整套支持的 USB 类设备）。

在编写本章时（2022 年 1 月），ST 刚刚发布了 STM32H7 和 STM32F4 的 X-CUBE 扩展包。根据作者介绍，ST 需要一年多的时间才能完成整个 STM32 产品线的集成。此外，目前还不清楚 RTOS 市场在未来几年将如何演变。因此，本书将仅涵盖 FreeRTOS，将涵盖 Azure RTOS 的可能性留给书中未来的更新。

### 23.1 理解 RTOS 的底层概念

> 本段快速介绍了实时操作系统的底层核心概念。经验丰富的用户可以跳过此处，除非。

除了中断服务程序（ISR）和异常处理程序外，到目前为止的所有示例都设计为我们的应用程序由单一执行流组成。通常，从 `main()` 例程开始，一个大型无限循环承载着固件任务：

```c
while(1) {

    doOperation1();
```
