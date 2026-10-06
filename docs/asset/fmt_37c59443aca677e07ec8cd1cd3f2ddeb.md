
| dmas | phandle-array | DMA 通道指定符 |

| dma-names | string-array | DMA 通道指定符名称 |

| io-channels | phandle-array | IO 通道指定符 |

| io-channel-names | string-array | Mailbox/IPM 通道指定符 |

| mboxes | phandle-array | Mailbox/IPM 通道指定符 |

| mbox-names | string-array | 提供的/IPM 通道指定符名称 |

| Name | Type | Details |

| --- | --- | --- |

| wakeupsource | boolean | 用于标识设备可用唤醒源的属性。提供此属性时，设备会设置特定标记，告诉系统该设备能够唤醒系统。唤醒能力设备默认被禁用（中断不会唤醒系统），但如有必要可以在运行时启用它们。 |

| power-domain | handle | 设备所属的电源域。当电源域处于挂起或恢复状态时，设备将收到通知。 |

对于 SPI 总线上的 bosch bme280，节点特定属性表如下：

| Name | Type | Details |

| --- | --- | --- |

| friendly-name | string | 描述传感器的易读字符串。可用于区分同一模型的多个实例。 |

| spi-max-frequency | int | SPI 接口的最大频率。此属性是必须的。 |

| duplex | int | 双工模式，全双工或半双工。默认始终全双工。 |

| Name | Type | Details |

| --- | --- | --- |

| format | int | Motorola 或 TI 格式。默认始终 Motorola。 |

| supply-gpios | handle-array | 控制电源的 GPIO 指定器。当设备具有专用电压调节器时，应提供此属性。 |

| vin-supply | handle | 指向控制设备电源的电压调节器的引用。当设备电源由共享电压调节器供电时，应提供此属性。 |

| Name | Type | Details |

|---|---|---|

| overruncharacter | int | 当 TX 缓冲区中的所有字节发送完毕，但由于 RX 的原因传输继续时，将使用溢出字符 (ORC)。默认值为 0xff（高电平），这是 SPI 传输中最常用的值。默认值：255 |

| clock-frequency | int | SPI 外设所运行的时钟频率，单位为 Hz。 |

# 第 9 章 通用设备树理解与使用

特别是 SPI 和 I2C

| Name | Type | Details |

|---|---|---|

| cs-gpios | phandlearray | 使用的片选（CS）GPIO 数组。数组中的每个元素指定一个 GPIO。数组中的索引对应控制该 CS GPIO 的子节点。 |

示例：

```
spi@... {
  cs-gpios = &gpio0 23 GPIO_ACTIVE_LOW,
  &gpi1 10 GPIO_ACTIVE_LOW;
  ...
spi-device@0 {
  reg = <0>;
  ...
}
spi-device@1 {
  reg = <1>;
  ...
}
}
```

子节点 `spi-device@0` 指定了一个使用片选控制器 `gpio0`、引脚 23 以及设备树 GPIO 标志 `GPIO_ACTIVE_LOW` 的 SPI 设备。同样，`spi-device@1` 具有 CS GPIO 控制器 `gpio1`、引脚 10 和标志 `GPIO_ACTIVE_LOW`。可以以相同的方式配置其他设备。

关于标志单元（cell），`GPIO_ACTIVE_LOW` 通常是 "Csn" 引脚的安全选择。如果中间硬件对外设设备反转了信号，或者该线路本身是高电平有效，则可以使用 `GPIO_ACTIVE_HIGH`。

如果此属性未定义，则未设置片选 GPIO。具有专用 CS 引脚的 SPI 控制器不需要定义 `cs-gpios` 属性。

## 第 9 章 通用设备树理解与使用，特别是 SPI 和 I2C

| Name | Type | Details |

|---|---|---|

| pinctrl-0 | phandles | 第一种状态的引脚配置。内容取决于所选引脚控制器驱动的实现。 |

| pinctrl-1 | phandles | 第二种状态的引脚配置。内容取决于所选引脚控制器驱动的实现。 |

| pinctrl-2 | phandles | 第三种状态的引脚配置。内容取决于所选引脚控制器驱动的实现。 |

| pinctrl-3 | phandles | 第四种状态的引脚配置。内容取决于所选引脚控制器驱动的实现。 |

| pinctrl-4 | phandles | 第五种状态的引脚配置。内容取决于所选引脚控制器驱动的实现。 |

| pinctrl-names | string-array | 提供状态的名称。名称数量与状态数量匹配。 |

| memory-phandle | array | 内存区域句柄（phandle）列表 |

| memory-region | string-array | 内存列表，memory-region 中的每个对应句柄对应一个名称。 |

对于 `cs-pios` 属性，必须提供片选的 GPIO 端口、引脚号和标志，如下代码段所示：

```
&spi3 {
  compatible = "nordic,nrf-spim";
  status = "okay";
  cs-pios = &gpio1 12 GPIO_ACTIVE_LOW>;
  mysensor: bme280@0 {
    compatible = "bosch,bme280";
    label = "BME280";
    reg = <0>;
}
```

在行 `cs-gpios = &gpio1 12 GPIO_ACTIVE_LOW>;` 中：

- `&gpio1` 指向 GPIO 端口

- `12` 是引脚号

- `GPIO_ACTIVE_LOW` 是一个有效标志

从前面的代码段可以推断出低电平有效驱动片选。Zephyr 有兼容 bme280 传感器的驱动，但该传感器并未内置。该节点是节点控制器的子节点。对于 SPI 设备，必须为特定传感器指定片选，这通过 `reg` 属性来实现。这里，`reg = <0>` 表示 `cs-pios` 属性的索引 0。

`mysensor`（第 5 行）是一个节点标签（label）……不要与 `label` 属性（第 6 行）混淆。在实现应用代码段时，可以使用其中任何一个来获取设备指针。

以下代码段展示了如何编写代码来获取设备结构体指针并使用该设备。它展示了宏 `DEVICE_DT_GET` 和宏 `DT_NODELABEL` 的使用。

```
const struct device *dev = DEVICE_DT_GET(DT_
NODELABEL(mysensor));
 (!device_is_ready(dev)) { return; }
struct sensor_sample_type dev;
sensor_sample_fetch(dev);
sensor_channel_get (dev, SENSOR_CHAN_AMBIENT_TEMP, &temp);
printk("temperature in degrees C: %d. %d\n", temp.val2);
```

## 第 9 章 通用设备树理解与使用，特别是 SPI 和 I2C

```
const struct device *dev = DEVICE_DT_GET(DT_
NODELABEL(mysensor));
 (!device_is_ready(dev)) { return; }
struct sensor_sample_type dev;
sensor_sample_fetch(dev);
sensor_channel_get (dev, SENSOR_CHAN_AMBIENT_TEMP, &temp);
printk("temperature in degrees C: %d. %d\n", temp.val2);
```

## 第 9 章 通用设备树理解与使用，特别是 SPI 和 I2C

```
const struct device *dev = DEVICE_DT_GET(DT_
NODELABEL(mysensor));

device_is_ready(dev)) { return; }
struct sensor_sample_type dev;
sensor_sample__(dev);
sensor_channel_get (dev, SENSOR_CHAN_AMBIENT__, &,


temperature in
in: ....n.
..
);
```

## 第 9 章 通用设备树理解与使用，特别是 SPI 和 I2C

```
const struct device *dev = DEVICE_DT_GET(DT_
NODELABEL(mysensor));
 (!device_is_ready(dev)) { return; }
struct sensor_sample_type dev;
sensor_sample_fetch(dev);
sensor_channel_get (dev, SENSOR_CHAN_AMBIENT_TEMP, &temp);
printk("temperature in degrees C: %d. %d\n", temp.val2);
```

## 第 9 章 通用设备树理解与使用，特别是 SPI 和 I2C

```
const struct device *dev = DEVICE_DT_GET(DT_
NODELABEL(mysensor));
 (!device_is_ready(dev)) { return; }
struct sensor_sample_type dev;
sensor_sample_fetch(dev);
sensor_channel_get (dev, SENSOR_CHAN_AMBIENT_TEMP, &temp);
printk("temperature in degrees C: %d. %d\n", temp.val2);
```

## 第 9 章 通用设备树理解与使用，特别是 SPI 和 I2C

```
const struct device *dev = DEVICE_DT_GET(DT_
NODELABEL(mysensor));
 (!device_is_ready(dev)) { return; }
struct sensor_sample_type dev;
sensor_sample_fetch(dev);
sensor_channel_get (dev, SENSOR_CHAN_AMBIENT_TEMP, &temp);
printk("temperature in degrees C: %d. %d\n", temp.val2);
```

## 第 9 章 通用设备树理解与使用，特别是 SPI 和 I2C

```
const struct device *dev = DEVICE_DT_GET(DT_
NODELABEL(mysensor));
 (!device_is_ready(dev)) { return; }
struct sensor_sample_type dev;
sensor_sample_fetch(dev);
sensor_channel_get (dev, SENSOR_CHAN_AMBIENT_TEMP, &temp);
```

502

## 第 9 章 通用设备树理解与使用，特别是 SPI 和 I2C

```
const struct device *dev = DEVICE_DT_GET(DT_
NODELABEL(mysensor));
 (!device_is_ready(dev)) { return; }
struct sensor_sample_type dev;
sensor_sample_fetch(dev);
sensor_channel_get (dev, SENSOR_CHAN_AMBIENT_TEMP, &temp);
```

503

## 第 9 章 通用设备树理解与使用，特别是 SPI 和 I2C

```
const struct device *dev = DEVICE_DT_GET(DT_
NODELABEL(mysensor));
 (!device_is_ready(dev)) { return; }
struct sensor_sample_type dev;
sensor_sample_fetch(dev);
sensor_channel_get (dev, SENSOR_CHAN_AMBIENT_TEMP, &temp);
```

504

# 第 9 章理解和使用设备树（Devicetree），特别是 SPI 和 I2C

展开宏定义

```
DEVICE_DT_INST_DEFINE(inst, \
bme280_chip_init, \
PM_DEVICE_DT_INST_REF(inst), \
&bme280_data_data##inst, \
&bme280_config##inst, \
POST_KERNEL, \
CONFIG_SENSOR_INIT_PRIORITY, \
&bme280_api_funcs);
```

涉及到对 `##` 拼接运算符的使用，其在这里的目的是生成具有唯一名称的全局变量，这种唯一性实际上来自于驱动程序中设备树中的信息，因此全局变量令牌（token）中包含了序数 63。

该序数是枚举设备树中节点的结果。每个节点都将关联一个不同的序数，这确保了设备将与唯一命名的全局变量关联。

在多实例驱动应用的情况下，将存在多个来自不同设备树节点的不同 `struct devices` 结构体，它们具有相同的 `compatible`（兼容性属性）。下面的示例说明了涉及两个兼容属性的情况：一个用于连接到 I2C 总线的设备，另一个用于连接到 SPI 总线的设备。

```
spi3 {
  /* ... */
  onspi: bme280@0 {
    compatible = "bosch, bme280";
    label = "BME280"
    reg = <0>
    spi-max-frequency = <1000000>
  };
}
```

驱动宏的展开将在要编译的 C 文件中创建具有唯一名称的设备全局变量，如下所示：

```
const struct device __device_dts_ord_65 = {
  ...
```

```
const struct device __device_dts_ord_70 = {
  ...
```

需要注意的是，实例号（instance numbers）并不是序数（ordinal numbers）。在接下来的示例中，实例号是 0 和 1。在应用中，将根据宏展开产生两个设备。以下代码的宏展开：

```
const struct device
  *spidev = DEVICE_DT_GET(DT_NODELABEL(onspi)),
  *i2cdev = DEVICE_DT_GET(DT_NODELABEL(oni2c));
```

结果如下：

```
const struct device
  *spidev = (&_device_dts_ord_70);
  *i2cdev = (&_device_dts_ord_65);
```

设备树处理生成一个头文件，在头文件中预先声明所有可能的设备，这样应用开发者在获取它们的地址之前无需手动声明它们。

从代码角度来看，结果的内存占用与访问全局数据结构的情况相同。然而，基于宏的方法结合了分层配置语言，而又不会引入显式执行树遍历（tree-walking）带来的内存占用和性能代价。

总之，基于设备树的设计实现了以下：

- 设备树捕捉了依赖关系，且这些依赖信息在编译时可用。

- 序数捕捉了设备树的依赖结构，且这些依赖信息在预处理器阶段可用。

- 还有设备树 API 用于查询节点的正向和反向依赖，并且在设备结构中提供依赖信息，使得在链接时控制设备初始化步骤的顺序成为可能，从而在应用程序运行时，设备按正确的顺序进行初始化。

- 了解设备依赖关系对于设备电源管理也同样重要，因为它有助于确保按正确顺序关闭，例如在进入睡眠模式时。

## I2C 案例研究示例

此示例基于 X-NUCLEO-IKS01A2 板板，这是一块用于 STM32 Nucleo 的运动 MEMS 和环境传感器扩展板，带有 Arduino UNO R3 接口。它包含了多种传感器，即 LSM6DSL 3D 加速度计和 3D 陀螺仪、LSM303AGR 3D 加速度计和 3D 磁计，以及 HTS221 湿度温度传感器，X-NUCLEO-IKS01A2 通过 I2C 与 STM32 微控制器接口。

图 9-11 显示了该板的图像。

![](img/d625a3dc80e999570aa2c88dcc398b17_508_0.png)

图 9-11。X-NUCLEO-IKS01A2 板图像
