

在任何加载时，驱动程序都会创建设备对象来表示逻辑或物理设备——即使是驱动程序的逻辑接口或端点——这将调用 `IoCreateDevice` 或 `IoCreateDeviceSecure`。然而，即插用（PnP）驱动程序会在 PnP Manager通知它们存在需要管理的设备时，在其 `add-device` 例程中创建设备。相反，非即插用驱动程序通常在 I/O Manager调用其初始化例程时创建设备。当驱动程序的最后一个设备对象被删除且没有对驱动程序的引用时，I/O Manager会卸载该驱动程序。

驱动程序与其设备对象之间的关系如图 6-10 所示。

![](img/ff0e6a9d867a3a6e9527eb1d946810fc_517_0.png)

**图 6-10** 驱动程序及其设备对象。

驱动程序在 `DeviceObject` 成员中持有指向第一个设备对象的指针。第二个设备对象由 `DEVICE_OBJECT` 的 `NextDevice` 成员指向，直到最后一个指向 `NULL`。每个设备对象都通过 `DriverObject` 成员指向回驱动程序。图 6-10 中显示的所有箭头都是由设备创建函数（`IoCreateDevice` 或 `IoCreateDeviceSecure`）构建的。所示的 `DeviceExtension` 指针是驱动程序可以为其管理的每个设备分配额外内存的一种方式。

> 注意：区分驱动对象和设备对象至关重要。驱动对象代表驱动程序的行为，而单个设备对象代表通信端点。例如，在一个具有四个串口的系统上，将有一个驱动对象（以及一个二进制文件），但会有四个设备对象实例，每个实例代表一个端口，可以单独打开而不影响其他串口。对于设备而言，每个设备还代表了一组不同的硬件资源，如 I/O 端口、内存映射 I/O 和中断线。Windows 是以设备为中心，而不是以驱动程序为中心。

当驱动程序创建设备对象时，驱动程序可以选择地为该设备分配一个名称。名称会将设备对象放在设备对象命名空间中。驱动程序可以显式定义设备名称，也可以由 I/O Manager 自动生成。按照惯例，设备对象被放在命名空间中的 `\Device` 目录（，使用 Windows API 的应用程序无法访问该目录）。

注意：某些驱动程序会将设备对象放在 `\Device` 以外的目录。例如，IDE 驱动程序在 `\Device` 目录中创建代表 IDE 端口和通道的设备对象。请参见第二部分的第12章关于存储架构的描述，包括驱动程序使用设备对象的方法。

如果驱动程序需要允许应用程序打开设备对象，它必须在 `\GLOBAL\` 中创建一个指向 `\Device` 目录下设备对象名称的符号链接。（非即插用和文件系统驱动程序通常使用 `IoCreateSymbolLink` 函数创建一个已知名称的符号链接（例如 `\Device\HarddiskVolume2`）。由于已知名称在硬件动态出现和消失的环境中工作得不好，PNP 驱动程序通过调用 `IoRegisterDeviceInterface` 函数来暴露一个或多个接口，并指定一个全局唯一标识符（GUID）。GUID 是 128 位的值，可以使用 `uuguid` 和 `guididen` 等工具生成，这些工具包含在 WDK 和 Windows SDK 中。鉴于 128 位所表示的数值范围（以及生成它们的公式），从统计学上来说，几乎可以确定每个 GUID 都是全局唯一的。

`IoRegisterDeviceInterface` 生成与设备实例相关的符号链接。然而，在 I/O Manager 创建接口之前，驱动程序必须调用 `SetDeviceInterface` 来启用设备的接口。通常在 PnP Manager 通过发送驱动程序设备 IRP 启动设备时执行——在这种情况下是带有 `IRP_MN_START_DEVICE`（次函数代码）的 `IRP_MJ_PNP`（主函数代码）。IRP 将在本章稍后的“I/O 请求”部分进行讨论。

想要打开用 GUID 表示接口的设备对象的应用程序，可以在用户空间调用即插用设置函数，例如针对特定 GUID 调用 `SetupEnumInterfaces` 以获取其可用于打开设备对象的符号链接名称。对于 `SetupEnumInterfaces` 报告的每个设备，应用程序执行 `SetupGetDeviceDetail` 以获取有关设备的更多信息，例如其自动生成的名称。从 `SetupGetDeviceInterface` 获取设备名称后，应用程序可以执行 Windows 的 `CreateFile` 或 `CreateFile2` 来打开并获取设备。

## 实验：查看设备对象

你可以使用 Sysinternals 的 WinObj 工具或 `!kernel` 调试器命令查看对象管理器命名空间下 `\Device` 的设备名称。以下显示了 I/O Manager 分配给 `\Device` 中自动生成名称的设备对象的符号链接：

```
1: kd \device
Object: 8200c530 (8542b188) Directory
ObjectHeader: 8200c518 (new version)
HandleCount: 0 PointerCount: 231
Directory: 82007d20

## 设备管理器

| Name | Type | SymbolLink |
| --- | --- | --- |
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
| HKLM\SYSTEM\CurrentControlSet\Enum\USB\VID_046D&PID_C52B\Instance_82b8c5d0-0000-11d0-8015-00a0cde00006 | Device | \Device#VID_046D&PID_C52B|
```

当你运行设备查询并指定 `\Device` 目录时，它的输出应该类似于以下内容：

```
1: kd \device
Object: 8200c530 (8542b188) Directory
ObjectHeader: 8200c518 (new version)
HandleCount: 0 PointerCount: 231
Directory: 82007d20
```

