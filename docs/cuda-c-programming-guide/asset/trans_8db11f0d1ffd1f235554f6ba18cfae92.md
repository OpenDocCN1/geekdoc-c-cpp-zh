

### 3.2.5.7.2. 已用时间

在 Creation and Destruction 中创建的事件可用于以下方式对 Creation and Destruction 的代码示例进行计时：

```
cudaEventRecord(start, 0);
for (int i = 0; i < 2; i++) {
    cudaMemcpyAsync(inputDev + i * size, inputHost + i * size,
                    size, cudaMemcpyHostToDevice, stream[i]);
    MyKernel<<<100, 512, 0, stream[i]>>>
    (outputDev + i * size, inputDev + i * size, size);
    cudaMemcpyAsync(outputHost + i * size, outputDev + i * size,
                    size, cudaMemcpyDeviceToHost, stream[i]);
}
cudaEventRecord(stop, 0);
cudaEventSynchronize(stop);
float elapsedTime;
cudaEventElapsedTime(&elapsedTime, start, stop);
```

### 3.2.5.8. 同步调用

调用同步函数时，在设备完成请求的任务之前，控制权不会返回到主机线程。主机线程随后是否会让出、阻塞或自旋，可以在主机线程执行任何其他 CUDA 调用之前，通过调用 cudaSetDeviceFlags() 并传入特定标志来指定（有关详细信息，请参阅参考手册）。

## 3.2.6. 多设备系统

### 3.2.6.1. 设备枚举

主机系统可以拥有多个设备。以下代码示例展示了如何枚举这些设备、查询其属性，并确定 CUDA 支持设备的数量。

```
int deviceCount;
cudaGetDeviceCount(&deviceCount);
int device;
for (device = 0; device < deviceCount; ++device) {
    cudaDeviceProp deviceProp;
    cudaGetDeviceProperties(&deviceProp, device);
    printf("Device %d has compute capability %d.%d.\n",
           device, deviceProp.major, deviceProp.minor);
}
```

### 3.2.6.2. 设备选择

主机线程可以随时通过调用 cudaSetDevice() 设置其操作的设备。设备内存分配和内核启动在当前设置的设备上进行；流和事件与当前设置的设备关联创建。如果未调用 cudaSetDevice()，则当前设备为设备 0。

以下代码示例说明设置当前设备如何影响内存分配和内核执行。

```
size_t size = 1024 * sizeof(float);
cudaSetDevice(0); // Set device 0 as current
float* p0;
cudaMalloc(&p0, size); // Allocate memory on device 0
MyKernel<<<1000, 128>>>(p0); // Launch kernel on device 0
cudaSetDevice(1); // Set device 1 as current
float * p1;
cudaMalloc(&p1, size); // Allocate memory on device 1
MyKernel<<<1000, 128>>>(p1); // Launch kernel on device 1
```

### 3.2.6.3. 流和事件行为

如果向与当前设备未关联的流发出内核启动，则会失败，如以下代码示例所示。

```
cudaSetDevice(0); // Set device 0 as current
cudaStream_t s0;
cudaStreamCreate(&s0); // Create stream s0 on device 0
MyKernel<<<1000, 64, 0, s0>>>(); // Launch kernel on device 0 in s0
cudaSetDevice(1); // Set device 1 as current
cudaStream_t s1;
cudaStreamCreate(&s1); // Create stream s1 on device 1
MyKernel<<<1000, 64, 0, s1>>>(); // Launch kernel on device 1 in s1
// This kernel launch will fail:
MyKernel<<<1000, 64, 0, s0>>>(); // Launch kernel on device 1 in s0
```

即使向与当前设备未关联的流发出内存拷贝，也会成功。

如果输入事件和输入流关联到不同的设备，**cudaEventRecord()** 将失败。

如果两个输入事件关联到不同的设备，**cudaEventElapsedTime()** 将失败。

即使输入事件关联到与当前设备不同的设备，**cudaEventSynchronize()** 和 **cudaEventQuery()** 也会成功。

即使输入流和输入事件关联到不同的设备，**cudaStreamWaitEvent()** 也会成功。因此，**cudaStreamWaitEvent()** 可用于多个设备之间的同步。

每个设备都有自己的默认流（请参阅默认流），因此发送到设备默认流的命令可能会相对于发送到任何其他设备默认流的命令乱序执行或并发执行。

### 3.2.6.4. 对等内存访问

取决于系统属性，特别是 PCIe 和/或 NVLINK 拓扑，设备能够相互寻址对方的内存（即，在一个设备上执行的内核可以解引用指向另一设备内存的指针）。如果 **cudaDeviceCanAccessPeer()** 对这两个设备返回 true，则这两个设备之间支持此对等内存访问功能。

对等内存访问仅在 64 位应用程序中受支持，并且必须通过调用 **cudaDeviceEnablePeerAccess()** 在两个设备之间启用，如以下代码示例所示。在未启用 NVSwitch 的系统上，每个设备最多支持系统范围内的八个对等连接。

两个设备使用统一地址空间（请参阅统一虚拟地址空间），因此可以使用相同的指针来寻址两个设备的内存，如以下代码示例所示。

```
cudaSetDevice(0);    // Set device 0 as current
float * p0;
size_t size = 1024 * sizeof(float);
cudaMalloc(&p0, size);    // Allocate memory on device 0
MyKernel<<<1000, 128>>>(p0);    // Launch kernel on device 0
cudaSetDevice(1);    // Set device 1 as current
cudaDeviceEnablePeerAccess(0, 0);    // Enable peer-to-peer access
// with device 0

// Launch kernel on device 1
// This kernel launch can access memory on device 0 at address p0
MyKernel<<<1000, 128>>>(p0);
```

### 3.2.6.4.1. Linux 上的 IOMMU

仅在 Linux 上，CUDA 和显示驱动程序不支持启用 IOMMU 的裸机 PCIe 对等内存拷贝。但是，CUDA 和显示驱动程序通过 VM 直通支持 IOMMU。因此，在 Linux 上运行原生裸机系统的用户应禁用 IOMMU。应启用 IOMMU，并应将 VFIO 驱动程序用作虚拟机的 PCIe 直通。

在 Windows 上，上述限制不存在。

另请参阅 64 位平台上的 DMA 缓冲区分配。

### 3.2.6.5. 对等内存拷贝

可以在两个不同设备的内存之间执行内存拷贝。

当两个设备使用统一地址空间时（请参阅统一虚拟地址空间），这是使用设备内存中提到的常规内存拷贝函数完成的。

否则，这是使用 cudaMemcpyPeer()、cudaMemcpyPeerAsync()、cudaMemcpy3DPeer() 或 cudaMemcpy3DPeerAsync() 完成的，如以下代码示例所示。

```
cudaSetDevice(0);    // Set device 0 as current
float * p0;
size_t size = 1024 * sizeof(float);
cudaMalloc(&p0, size);    // Allocate memory on device 0
cudaSetDevice(1);    // Set device 1 as current
float * p1;
cudaMalloc(&p1, size);    // Allocate memory on device 1
cudaSetDevice(0);    // Set device 0 as current
MyKernel<<<1000, 128>>>(p0);    // Launch kernel on device 0
cudaSetDevice(1);    // Set device 1 as current
cudaMemcpyPeer(p1, 1, p0, 0, size);    // Copy p0 to p1
MyKernel<<<1000, 128>>>(p1);    // Launch kernel on device 1
```

在两个不同设备的内存之间进行拷贝（在隐式 NULL 流中）：
- 在向任一设备发出的所有先前命令完成之前不会开始，并且
- 在拷贝之后向任一设备发出的任何命令（请参阅异步并发执行）开始之前运行到完成。

与流的正常行为一致，两个设备内存之间的异步拷贝可能与另一个流中的拷贝或内核重叠。

请注意，如果通过 `cudaDeviceEnablePeerAccess()` 在两个设备之间启用了对等访问（如对等内存访问中所述），则这两个设备之间的对等内存拷贝不再需要通过主机暂存，因此速度更快。

## 3.2.7. 统一虚拟地址空间

当应用程序作为 64 位进程运行时，主机和所有计算能力 2.0 及更高版本的设备使用单个地址空间。通过 CUDA API 调用进行的所有主机内存分配以及受支持设备上的所有设备内存分配都在此虚拟地址范围内。因此：

- 可以使用 `cudaPointerGetAttributes()` 从指针值确定通过 CUDA 在主机上分配的任何内存，或使用统一地址空间的任何设备上的任何内存的位置。
- 当向使用统一地址空间的任何设备的内存拷贝或从中拷贝时，可以将 `cudaMemcpy*()` 的 `cudaMemcpyKind` 参数设置为 `cudaMemcpyDefault` 以从指针确定位置。这也适用于未通过 CUDA 分配的主机指针，只要当前设备使用统一寻址。
- 通过 `cudaHostAlloc()` 进行的分配在使用统一地址空间的所有设备之间自动可移植（请参阅可移植内存），并且 `cudaHostAlloc()` 返回的指针可以直接从在这些设备上运行的内核中使用（即，无需通过 `cudaHostGetDevicePointer()` 获取设备指针，如映射内存中所述）。

应用程序可以通过检查 `unifiedAddressing` 设备属性（请参阅设备枚举）是否等于 1 来查询特定设备是否使用统一地址空间。

## 3.2.8. 进程间通信

由主机线程创建的任何设备内存指针或事件句柄都可以由同一进程中的任何其他线程直接引用。但是，它在此进程外无效，因此不能由属于不同进程的线程直接引用。

要跨进程共享设备内存指针和事件，应用程序必须使用进程间通信 API，该 API 在参考手册中有详细说明。IPC API 仅支持 Linux 上的 64 位进程以及计算能力 2.0 及更高版本的设备。请注意，IPC API 不支持 `cudaMallocManaged` 分配。

使用此 API，应用程序可以使用 `cudaIpcGetMemHandle()` 获取给定设备内存指针的 IPC 句柄，并使用

