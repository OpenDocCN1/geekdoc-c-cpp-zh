

- 4. “激活”飞区所需的最后一步是通过 `InitializeEnclave` 函数实现的。此时，配置已配置为在飞区内执行的代码就可以开始执行了。
- 5. 遗憾的是，在飞区中执行代码并没有被 API 封装。需要直接使用汇编语言。`ENTER` 指令强制执行跳转到飞区，而 `EXIT` 指令则返回调用函数。飞区也可能通过异步飞区退出（AEX）发生异常终止，例如页错误。具体细节超出了本书的讨论范畴，因为它们不是 Windows 特有的。请参阅 SGX 文档以获取最终细节。
- 6. 最后，要销毁飞区，可以使用从 `CreateEnclave` 获取的飞区指针调用普通的 `VirtualFree (Ex)` 函数。

## 内存初始化

在启动期间，Winload（Windows 启动加载器）调用 `Os1EnclavePageRegions`，该函数首先检查 CPUID 是否支持 SGX。如果支持，它会发出指令来枚举飞区页缓存（EPC）描述符。EPC 是处理器为分页和飞区提供的受保护内存。对于每个枚举的 EPC，`Os1EnclavePageRegions` 调用 `Mm-AddEnclavePageEnclaveMemory` 将页范围添加到类型为 `Loader_PARAMETER_BLOCK` 的内存描述符排序列表中。此列表最终存储在 `LOADER_PARAMETER_BLOCK` 结构的 `MemoryDescriptorListHeader` 中，用于将信息从启动加载器传递到内核。

在阶段 1 初始化期间，调用内存管理器 `CreateEnclaveRegions` 为发现的飞区区域创建一个 AVL 树（以便在需要时查找）；该树存储在 `MiState.Hardware.Enclave` 数据中。内核获取一个新的飞区页列表，一个特殊标志 `InsertPageFreeOrZeroList` 启用使用此列表的功能。然而，由于内存管理器没有标识符列表（8个值用了3个），内核实际上将这些页识别为当前发生页错误的“坏页”。内存管理器永远不会使用坏页，标记飞区页是为了防止被正常的内存管理操作使用，因此这些页最终进入坏页列表。

## 飞区构建

`CreateEnclave` API 结束调用内核中的 `NtCreateEnclave`。如所述，必须传入一个由 Intel SGX 在表 5-24 中设计的 SECS 结构。

`NtCreateEnclave` 首先通过查看 AVL 树（而不是使用 CPUID 指令）检查是否支持内存飞区。它会创建传入结构的副本（这是内核函数从用户态获取数据的惯例），如果飞区是在调用者不同的进程中创建的，则挂载到目标进程（`KeStackAttachProcess`）。然后它将控制权转移给 `MiCreateEnclave` 开始开始实际工作。

## 表 5-24 SECS 结构布局

| 字段 | 偏移量 (字节) | 大小 (字节) | 描述 |
| --- | --- | --- | --- |
| SIZE | 0 | 8 | 飞区的大小（字节）；必须是 2 的幂次 |
| BASEADR | 8 | 8 | 飞区基地址必须与大小自然对齐 |
| SSFRAMISE | 16 | 4 | 单个 SSA 帧的大小（字节）（包括 XSAVE、填充、GPR 和 MISC） |
| MRSIGNER | 128 | 32 | 测量寄存器，扩展了验证飞区的公钥。正确格式请参见 SIGSTRUCT |
| RESERVED | 160 | 96 | 飞区的产品 ID |
| ISVPROID | 256 | 2 | 飞区的安全版本号 (SVN) |
| ISVSN | 258 | 2 | 飞区标识符 |
| EID | 取决于实现 | 8 | 来自签的填充模式（用于密钥派生字符串） |
| PADDING | 取决于实现 | 352 | |
| RESERVED | 260 | 3836 | 包括 EID、其他非零保留字段和必须为零的字段 |

`MiCreateEnclave` 首先分配的是地址窗口扩展（AWE）信息，A API 也会使用该信息。这是由于 AWE 功能，飞区允许用户态应用程序直接访问物理页（即根据上述描述检测到的、作为 EPC 页的物理页）。每当用户态应用程序对物理页拥有直接控制权时，必须使用 AWE 数据结构和锁。这些数据存储在 `EPROCESS` 结构的 `AweInfo` 字段中。

接下来，`MiCreateEnclave` 调用 `MiAllocateEnclaveVAD` 来分配一个描述虚拟内存的飞区类型 VAD。此 VAD 具有 VAD 标记（像所有 VAD 一样），还有一个飞区标记，以便与真实的 VAD 区分来。最后，作为 VAD 分配的一部分，这是飞区内存的用户态地址所在地（如果在原始 `CreateEnclave` 调用中未显式指定）。

`MiCreateEnclave` 的下一步是获取一个关于飞区大小或初始提交的飞区页。这是因为根据 Intel SGX 文档，所有飞区都需要至少一个页控制结构与之关联。使用 `MiGetEnclavePage` 来获取描述所需的分配列表，并根据需要提取一个页。返回的页使用存储为飞区 VAD 部分的系统 PTE 进行映射；`MiInitializeEnclave` 函数返回相关的 PFN 数据结构并将其标记为 `ActiveAndValid`（活动且有效）。

并没有实际的位位可以帮助你区分飞区 PFN 与内存的任何其他区域（如非分页池）。这就是飞区 AVL 树派上用场的地方，`MI_PFN_IS_ENCLAVE` 是内核在每次需要检查 PFN 是否确实描述 EPC 区域时使用的函数。

PFN 初始化后，系统 PTE 转换为全局内核 PTE，并计算其结果性虚拟地址。`MiCreateEnclave` 的最后一步是调用 `KeCreateEnclave`，它现在将执行低级内核创建步骤，与实际的 SGX 硬件实现通信。`KeCreateEnclave` 的职责之一是在调用者未指定地址的情况下，填充 SECS 结构所需的基地址，它必须在与 SGX 硬件通信创建飞区之前在 SECS 结构中设置。

## 向飞区加载数据

一旦飞区创建完成，就到了向其加载信息的时间了。`LoadEnclaveData` 函数用于此目的。该函数仅将请求转发给底层的内核函数 `NtLoadEnclaveData`。该函数执行跨属性的内存拷贝操作。

如果使用 `CreateEnclave` 创建的飞区没有任何提交页，则必须先获取它们，这将向飞区添加零内存；否则，如果传递了初始预提交大小，则飞区的页可以直接从飞区外部填充非零内存。

由于飞区内存是由 VAD 描述的，传统的内存管理 API可以在此内存上部分工作。例如，对地址使用 `MEM_COMMIT` 标志调用 `NtAllocateVirtualMemory` 将导致 `MiCommitEnclavePages`，该函数将验证新页的保护是否兼容（即读、写、执行的组合，无特殊的缓存或写入标记），然后调用 `MiAddPagesToEnclave`，传递与地址范围相关的飞区 VAD 指针、`Virtualalloc` 指定的保护掩码以及对应的 PTE 地址。

`MiAddPagesToEnclave` 检查 VAD 是否关联了 EPC 页，以及是否有足够的页满足提交。如果调用 `MiReserveEnclavePages` 获取足够的数量，`MiReserveEnclavePages` 将查看当前的飞区页列表并计数。如果处理器提供的物理 EPC 页不足，则函数失败。否则，它循环调用 `MiGetEnclavePage` 获取所需的页。

对于每个检索到的 PFN，它被链接到飞区 VAD 中的 PFN 数组。本质上，这意味着一旦飞区 PFN 从飞区页列表中移除进入飞区并活动状态，飞区 VAD 就充当了活动飞区 PFN 的列表。

