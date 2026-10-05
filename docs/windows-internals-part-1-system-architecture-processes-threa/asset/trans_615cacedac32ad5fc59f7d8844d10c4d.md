

| 设备 | 类型 |
| :--- | :--- |
| 854fb50 设备 | KMDF0 |
| 95bb040 设备 | Process管理 (ProcessManagement) |
| 97ad9fe0 符号链接 | 命名管道重定向 (MailslotRedirect) |
| 84f0090 设备 | 0000036 |
| 84c6538 设备 | FakeVid5 |
| 8bf14e98 设备 | Video1 |
| 8bf2fe20 设备 | KeyboardClass1 |
| 89c32a0 设备 | 0000029 |
| 89c05030 设备 | Vol1grControl |
| VMBus 设备 | VMBus |

当你输入对象命令并指定一个对象管理器目录对象时，内核调试器会根据对象管理器内部组织对象的方式转储驱动程序的内容。为了快速查找，目录在哈希表中存储对象，并使用对象名的哈希值，因此输出将显示存储在目录哈希表每个桶（bucket）中的对象。

如图 6-10 所示，设备对象指向其驱动对象，这是 I/O 管理器在接收 I/O 请求时调用驱动例程的方式。它使用设备对象找到代表服务该设备的驱动程序的驱动对象。然后，通过原始请求中提供的函数代码索引到驱动对象。每个函数代码都对应一个驱动程序点（称为分发例程，dispatch routine）。

驱动对象通常与多个设备对象相关联。当驱动程序从系统中卸载时，I/O 管理器使用设备对象队列来确定哪些设备将受驱动程序移除的影响。

## 实验：显示驱动对象和设备对象

你可以使用 !devobj 和 !devobj 内核调试器命令显示驱动对象和设备对象。在下面的示例中，检查了键盘类驱动程序的驱动对象以及它的其中一个设备对象：

```
1: kd> !devobj kbdclass
Driver object (8a557520) is for:
\Driver\kbdclass
Driver Extension List: (id , addr)

Device Object list:
9f509648 8bf2fe20 8a541030
1: kd> !devobj
Device object (9f509648) is:
KeyboardClass2 \Driver\kbdclass DriverObject 8a557520
nCurrent Irp 00000000 Count 0 0000000b Flags 00000244
dacl 82090960 DevExt 9f509700 DevExt 9f5097f0
ExtensionFlags (0x00000c00) DOE_SESSION_DEVICE, DOE_DEFAULT_PRESENT
Characteristics (0x00001000) FILE_DEVICE_SECURE_OPEN
AttachedTo(Lower) 9F509848 \Driver\internpt
Device is not busy.
```

注意，drob 命令还会向你显示正在查看的对象所叠加任何设备对象的地址和名称（AttachedTo 行）。它还可以显示叠加在指定对象之上的设备对象（AttachedDevice 行），尽管在本例中并非如此。

drob 命令可以接受一个可选参数，指示要显示的更多信息。这里是一个显示最多信息的示例：

```
1: kd> drobj kbclass 7
Driver object (8a5572d0) is for:
\Driver\kbclass
 Extension List: (id , addr)

Device Object list:
9F509648 8b2fe20 8a541030
```

| 字段 | 地址 |
| :--- | :--- |
| DriverEntry | 8c30a10 |
| DriverStartTo | 00000000 |
| DriverLoad | 00000000 kbdclass!KeyboardAddDevice |
| AddDevice: | 8c307250 |

| 分发例程 (Dispatch routines) | 地址 |
| :--- | :--- |
| [00] MJ_CREATE | 8c301d80 kbdclass!KeyboardClassCreate |
| [01] MJ_CREATE_NAMED_PIPE | 81a42342 nt!InvalidDeviceRequest |
| [02] MJ_CLOSE | 8c30c190 kbdclass!KeyboardClassClose |
| [03] MJ_READ | 8c302150 kbdclass!KeyboardClassRead |
| [04] MJ_WRITE | 81a42342 nt!InvalidDeviceRequest |
| [05] MJ_QUERY_INFORMATION | 81a42342 nt!InvalidDeviceRequest |
| [06] MJ_SET_INFORMATION | 81a42342 nt!InvalidDeviceRequest |
| [07] MJ_QUERY_EA | 81a42342 nt!InvalidDeviceRequest |
| [08] MJ_SET_EA | 8c30a10 kbdclass!KeyboardClassFlush |
| [09] MJ_FLUSH_BUFFERS | 8c306768 nt!InvalidDeviceRequest |
| [10] MJ_QUERY_VOLUME_INFORMATION | 81a42342 nt!InvalidDeviceRequest |
| [11] MJ_SET_VOLUME_INFORMATION | 81a42342 nt!InvalidDeviceRequest |
| [12] MJ_DIRECTORY_CONTROL | 81a42342 nt!InvalidDeviceRequest |
| [13] MJ_SYSTEM_CONTROL | 81a42342 nt!InvalidDeviceRequest |
| [14] MJ_DEVICE | 8c3076d0 kbdclass!KeyboardDevice |

| 控制 | 地址 |
| :--- | :--- |
| [09] MJ_INTERNAL_DEVICE_CONTROL | 8c30ff70 kbdclass!KeyboardPass |
| [10] MJ_SHUTDOWN | 81a42342 nt!InvalidDeviceRequest |
| [11] MJ_LOCK_CONTROL | 81a42342 nt!InvalidDeviceRequest |
| [12] MJ_CLEANUP | 8c302260 kbdclass!KeyboardClassCleanup |
| [13] MJ_CREATE_SLOT | 81a42342 nt!InvalidDeviceRequest |
| [14] MJ_QUERY_SECURITY | 81a42342 nt!InvalidDeviceRequest |
| [15] MJ_SET_SECURITY | 81a42342 nt!InvalidDeviceRequest |
| [16] MJ_POWER | 8c301440 kbdclass!KeyboardClassPower |
| [17] MJ_SYSTEM_CONTROL | 8c307f40 kbdclass!KeyboardClassSystem |
| [18] IRP_DEVICE_CHANGE | 81a42342 nt!InvalidDeviceRequest |
| [19] IRP_QUERY_VOLUME | 81a42342 nt!InvalidDeviceRequest |
| [1a] IRP_SET_VOLUME | 81a42342 nt!InvalidDeviceRequest |
| [1b] IRP_MJ_PNP | 8c301870 kbdclass!KeyboardPnP |

分发例程被清晰地显示，将在下一节中讨论。请注意，驱动程序不支持的操作将传递给 I/O 管理器的例程。!devobj 命令的地址对应一个 DRIVER_OBJECT，而 !devobj 命令的地址对应一个 DEVICE_OBJECT。你可以直接使用调试器查看这些结构。

```
1: kd nt!_driver_object 8a557520
+0000 Type : 4
+0002 Size : 0x168
+0004 DeviceObject : 0x9f509648 _DEVICE_OBJECT
+0008 Flags : 0x412
+00c0 DriverStart : 0xc30000 Void
+0010 DriverSize : 0x000
+0014 DriverSection : 0x8a557c8 _DRIVER_EXTENSION
+0018 DriverExtension : 0x8a557c8 _
+001c DriverName : _UNICODE_STRING "kbdclass"
+0024 Hardware_database : 0x815c2c22 _UNICODE_STRING "REGISTRY\MACHINE"
+0028 FastIo : (null)
+002c DriverInit : 0x30
+0030 MajorFunction : 7
+0034 DriverUnload : (null)
+0038 SectionName : (null)
+003c DeviceType : (null)
+0040 FileObjectType : (null)
+0044 InitialIrp : 0
+0048 SharedData : (null)
+004c Dpc : (null)
+0050 Timer : (null)
+0054 WaitObject : (null)
+0058 Flags : (null)
+005c Queue : _KDEVICE_QUEUE
+0060 StackSize : 0
+0064 ActiveThreadCount : 0
+0068 SecurityDescriptor : (null)
+006c DeviceObject : (null)
+0070 DeviceFlags : 0
+0074 DriverExtension : (null)
+007c DriverName : (null)
+0080 DriverStart : (null)
+0084 DriverSize : (null)
+0088 DriverSection : (null)
+008c SectionName : (null)
+0090 SectionObject : (null)
+0094 SectionObject : (null)
+0098 SectionObject : (null)
+009c SharedData : (null)
+00a0 DeviceType : (null)
+00a4 DeviceType : (null)
+00a8 FileObjectType : (null)
+00ac FileObjectType : (null)
+00b0 DeviceObject : (null)
+00b4 DeviceFlags : (null)
+00b8 DeviceExtension : (null)
+00bc DriverName : (null)
+00c0 DriverStart : 0xc30000 Void
+00c4 DriverSize : 0x000
+00c8 DriverSection : 0x8a557c8 _DRIVER_EXTENSION
+00cc DriverExtension : 0x8a557c8 _
+00d0 DriverName : _UNICODE_STRING "kbdclass"
+00d4 Hardware_database : 0x815c2c22 _UNICODE_STRING "REGISTRY\MACHINE"
+00d8 FastIo : (null)
+00de DriverInit : 0x30
+00e0 MajorFunction : 7
+00e4 DriverUnload : (null)
+00e8 SectionName : (null)
+00ec SharedData : (null)
+00f0 DeviceType : (null)
+00f4 DeviceType : (null)
+00f8 FileObjectType : (null)
+00fc FileObjectType : (null)
+0100 Type : 4
+0102 Size : 0x168
+0104 DeviceObject : 0x9f509648 _DEVICE_OBJECT
+0108 Flags : 0x412
+01c0 DriverStart : 0xc30000 Void
+0110 DriverSize : 0x000
+0114 DriverSection : 0x8a557c8 _DRIVER_EXTENSION
+0118 DriverExtension : 0x8a557c8 _
+011c DriverName : _UNICODE_STRING "kbdclass"
+0124 Hardware_database : 0x815c2c22 _UNICODE_STRING "REGISTRY\MACHINE"
+0128 FastIo : (null)
+012c DriverInit : 0x30
+0130 MajorFunction : 7
+0134 DriverUnload : (null)
+0138 SectionName : (null)
+013c SharedData : (null)
+0140 DeviceType : (null)
+0144 DeviceType : (null)
+0148 FileObjectType : (null)
+014c FileObjectType : (null)
+0150 DeviceObject : (null)
+0154 DeviceFlags : 0
+01158 DeviceExtension : (null)
+015bc DriverName : (null)
+0160 DriverStart : 0xc30000 Void
+0164 DriverSize : 0x000
+0168 DriverSection : 0x8a557c8 _DRIVER_EXTENSION
+016cc DriverExtension : 0x8a557c8 _
+0170 DriverName : _UNICODE_STRING "kbdclass"
+0174 Hardware_database : 0x815c2c22 _UNICODE_STRING "REGISTRY\MACHINE"
+0178 FastIo : (null)
+017c DriverInit : 0x30
+0180 MajorFunction : 7
+0184 DriverUnload : (null)
+0188 SectionName : (null)
+018c SharedData : (null)
+0190 DeviceType : (null)
+0194 DeviceType : (null)
+0198 FileObjectType : (null)
+019c FileObjectType : (null)
+01a0 DeviceObject : (null)
+01a4 DeviceFlags : 0
+01a8 DeviceExtension : (null)
```

分发例程被清晰地显示，将在下一节中讨论。请注意，驱动程序不支持的操作将传递给 I/O 管理器的例程。!devobj 命令的地址对应一个 DRIVER_OBJECT，而 !devobj 命令的地址对应一个 DEVICE_OBJECT。你可以直接使用调试器查看这些结构。

为了对使用文件对象的驱动代码保持某种程度的透明度，并允许在不扩大文件功能的情况下进行扩展，该结构还包含一个扩展字段，允许最多六种不同的附加属性，见表 6-2。

打开设备

文件对象是表示设备句柄的内核态数据结构。文件对象符合对象的标准：它们可以被多个进程共享；它们具有名称；受对象安全保护；并且支持同步。文件对象提供了可以读取或写入的表示。表 6-1 列出了文件对象的属性。

| 属性 | 目的 |
| :--- | :--- |
| 文件名 | 文件对象指向的文件，通过 CreateFile 或 CreateFile2 传递 |
| 当前字节偏移量 | 它在文件中的位置（仅用于同步 I/O） |
| 共享模式 | 这些指示当当前调用者使用时，其他调用者是否可以读取、写入或删除 |
| 打开模式 | 这些指示 I/O 是同步还是异步、缓存还是非顺序等 |
| 指向设备对象 | 标识文件所在的设备类型 |
| 指向卷块 (VPB) | 标识文件所在的卷或分区（文件系统情况下） |
| 指向节对象指针 | 这是一个描述映射/缓存文件的根结构。该结构还包含缓存映射，标识文件的哪些部分被缓存管理器缓存，以及它们在缓存中的位置 |
| 指向私有缓存映射 | 用于存储此句柄的页缓存信息或进程页优先级。参见第 5 节“内存管理”有关页优先级的信息 |
| I/O 请求包 (IRP) 列表 | 如果是线程 I/O（在本章后面的“线程异步 I/O”部分描述）且文件对象与完成部分相关（在“I/O 完成端口”部分描述），则这是与该文件相关的所有操作列表 |
| I/O 完成上下文 | 这是当前 I/O 完成部分的上下文信息（如果存在） |
| 文件对象扩展 | 存储文件的 I/O 优先级（在本章稍后解释）以及是否对文件对象执行共享访问检查，并包含存储特定上下文的可选文件扩展 |

为了对使用文件对象的驱动代码保持某种程度的透明度，并允许在不扩大文件功能的情况下进行扩展，该结构还包含一个扩展字段，允许最多六种不同的附加属性，见表 6-2。

