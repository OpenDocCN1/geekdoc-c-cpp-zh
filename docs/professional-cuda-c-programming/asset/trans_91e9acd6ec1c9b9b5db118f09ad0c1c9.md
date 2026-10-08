
由于 PCIe 支持任意两个节点之间的全双工通信，你可以使用异步拷贝函数执行双向的、对点的内存拷贝：

```
// bidirectional asynchronous memcopy copy
cudaEventRecord(start, 0);
for (int i = 0; i < 100; i++) {
    cudaMemcpyAsync(d_src[i], iBytes, cudaMemcpyDeviceToDevice, stream[0]);
    cudaMemcpyAsync(d_rcv[i], d_rcv[1], iBytes, cudaMemcpyDeviceToDevice, stream[1]);
}
```

双向内存拷贝测试实现在同一个文件中。以下是示例输出：

Ping-pong bidirectional cudaMemcpyAsync: 13.39ms performance: 10.02 GB/s

注意，所获得的带宽翻了一倍，因为 PCIe 总线同时被两个方向使用。如果你通过移除对 enableP2P 的调用来禁用对点访问，单向和双向示例仍能无错误地完成，但由于传输通过主机内存进行，测得的带宽将会下降。

## 使用统一虚拟寻址的对点内存访问

第 4 章引入的统一虚拟寻址（UVA）将 CPU 系统内存和设备全局内存映射到单一虚拟地址空间，如图 9-2 所示。通过 `cudaHostAlloc` 进行的主机内存分配以及通过 `cudaMalloc` 进行的设备内存分配位于此统一地址空间内。内存地址所在的设备可以从地址本身确定。

![](img/506ba3a4c9f4512233692f3f20de1f3a_425_0.png)

图 9-2

将对点 CUDA API 与 UVA 结合，可以对任何设备上的内存进行透明访问。你不需要手动管理内存缓冲区或从主机内存进行显式拷贝。底层使得显式执行这些操作成为可能，从而简化代码。注意，过度依赖 UVA 执行对点访问可能会产生负面影响，跨越 PCIe 总线的许多微小传输开销是巨大的。

以下代码演示了如何检查设备是否支持寻址：

```
int deviceID = 0;
cudaGetDeviceProperties(&prop, deviceID);
printf("GPU%d: %s addressing\n", deviceID, prop.unifiedAddressing ? "does not support");
```

要使用 UVA，应用程序必须在 64 位架构上编译，具有计算能力为 2.0 或更高的设备，并安装了 CUDA 4.0 或更高版本。如果同时启用对点访问和 UVA，内核可以引用指向另一个设备内存的指针。

你可以使用简单的内核（它将输入数组缩放 2，并将结果存储在输出数组中），从 GPU 测试对点内存访问：

```
__global void kernel(float* src, float* dst) {
  const int idx = blockIdx.x * blockDim.x + threadIdx.x;
  dst[idx] = src[idx] * 2.0f;
}
```

以下代码将 0 设置为当前设备，并使用指针 `d_src[0]` 从设备 1 读取全局内存，通过全局内存指针 `d_rcv[0]` 将结果写入当前设备：

```
cudaSetDevice(0);
kernel<<<grid,block>>>(d_rcv[0], d_src[0]);
```

以下代码将 1 设置为当前设备，并使用指针 `d_src[0]` 从设备 0 读取全局内存，通过全局内存指针 `d_rcv[1]` 将结果写入当前设备：

```
cudaSetDevice(1);
kernel<<<grid,block>>>(d_rcv[1], d_src[0]);
```

这些代码包含在 `simple P2P_PingPong.cu` 中。以下输出表明内核运行成功：

- 2. 正在 GPU1 上运行内核，从 GPU0 获取源数据并写入 GPU...
- 3. 正在 GPU0 上运行内核，从 GPU1 获取源数据并写入 GPU0...

如果你的 GPU 未连接到同一个 PCIe 根节点，或者禁用了对点访问，则将显示以下错误信息：

- > GPU disabled direct access to GPU1
> GPU1 disabled direct access to GPU0

## 多 GPU 上的有限差分

在本节中，你将学习如何通过使用有限差分方案求解 2D 波方程来跨设备重叠计算和通信。此示例扩展了之前向量加法和乒乓球示例中的概念，因为它包含了大量的计算和通信操作。注意，虽然示例的物理方程和术语包含在本章中，但不需要在数学上理解该问题。所有概念将从 CUDA 编程的角度进行解释；领域特定信息提供给好奇的读者。

## 2D 波方程的算子计算

2D 波传播由以下波方程控制：

$$\frac{\partial^2u}{\partial x^2} + \frac{\partial^2u}{\partial y^2}=v^2\frac{\partial^2u}{\partial t^2}$$

其中 $u(x, y, t)$ 是波场，$v(x, y)$ 是介质的传播。这是一个二阶偏微分方程。求解此类偏微分方程的常用方法是在笛卡尔网格上使用有限差分方案。

简单来说，有限差分方案使用模板（类似于第 5 章中演示的，尽管是二维的）来近似导数，通过对围绕该单点的多个局部点应用一个函数，来计算规则网格上单点的导数。图 9-3 展示了本节将作为示例的 17 点模板。为了评估中心点的导数，使用了距离中心点最近的 16 个局部点。

![](img/506ba3a4c9f4512233692f3f20de1f3a_427_0.png)

图 9-3

在计算上，偏导可以用泰勒展开表示，其在稠密形式中的实现如下面的伪代码所示。该伪代码使用数组 `der_u` 来累积来自当前元素 `u[i]`、前四个元素 `u[i+d]` 和后四个元素 `u[i-d]` 的贡献。`c` 数组存储导数系数，`u[i]` 是中心点，`der_u[i]` 是评估后的中心点导数。

```
der_u[i] = c[0] * u[i];
for(int d = 1; d <= 4; d++) {
  der_u[i] += c[d] * (u[i-d] + u[i+d]);
}
```

## 多 GPU 程序的典型模式

为了模拟波在不同介质中的传播，需要海量数据。这可能导致单个 GPU 的全局内存不足以存储仿真状态。这需要在多个 GPU 上对数据进行领域分解。假设 x 维度是 2D 数组的最内层维度。由于给定点的计算需要两侧最近的四个点，你需要为每个 GPU 存储的数据添加填充，即光区域（halo region）。

使用图 9-5 所示的领域分解，使用多个 GPU 求解波方程每一步都遵循这种通用模式：

- 1. 在一个流中计算光区域并与相邻 GPU 光数据。
- 2. 在另一个流中计算内部区域。
- 3. 在继续下次迭代之前同步所有设备上的计算。

![](img/506ba3a4c9f4512233692f3f20de1f3a_428_0.png)

图 9-4

![](img/506ba3a4c9f4512233692f3f20de1f3a_429_0.png)

图 9-5

如果你使用两个不同的流，一个用于光计算和通信，另一个用于内部区域的计算，则步骤 1 可以与步骤 2 重叠。如果内部计算所需的计算时间大于光操作所需的时间，你可以通过隐藏光通信对性能的影响，利用多个 GPU 实现线性加速。

使用两个 GPU 进行算子计算的伪代码代码所示：

```
for (int istep = 0; istep < nsteps; istep++) {
  // calculate halo in stream_halo
  for (int i = 0; i < 2; i++) {
    cudaDevice(i);
    2dfd_kernel<<<..., stream_halo[i]>>>(...);
  }
```

```
// exchange halo on stream_halo
cudaMemcpyAsync(..., cudaMemcpyDeviceToDevice, stream_halo[0]);
cudaMemcpyAsync(..., cudaMemcpyDeviceToDevice, stream_halo[1]);
```

```
// calculate the internal region in stream_internal
for (int i = 0; i < 2; i++) {
  cudaDevice(i);
  2dfd_kernel<<<..., stream_internal[i]>>>(...);
}
```

```
// synchronize before next iteration
for(int i = 0; i < 2; i++) {
  cudaDevice(i);
  cudaDevicesSynchronize();
}
```
