

# CUDA 调试

当内核中发生内存错误时，会出现 (cuda-gdb) 提示符。以下输出表示错误发生在 debug-segfault.cu 的第 34 行：

```
Program received signal CUDA_EXCEPTION_10, Device Illegal Address.
(Switching focus to CUDA kernel 1026, grid 1027, block (0,0,0), thread (0,0,0),
device 0, sm 1, warp 0)
kernel<<<1024,1,1>>>(arr=0xf0010000) at debug-segfault.cu:34
25
arr[tid] = foo(tid, id);
(cuda-gdb)
```

你可以使用 `list` 命令来查看源代码以获取上下文：

```
(cuda-gdb) list
28  global void kernel(int **arr) {
29      int tid = blockDim.x * threadIdx.x;
30      int i;
31

332      for (tid = tid; tid < N; tid++) {
33          for (i = 0; i < M; i++) {
34              arr[tid][i] = foo(tid, i);
35          }
36      }
37 }
(cuda-gdb)
```

发生地址的行报告在第 34 行。该行包含对输入 `arr` 的多级间引用。你可以通过打印 `arr[tid]` 中的地址来检查在偏移量 `tid` 处的 `arr` 内容：

```
(cuda-gdb) print arr[tid]
$1 = (@global *) 0x0
(cuda-gdb)
```

这无效。NULL 内存地址无法被解引用。你可以尝试在 cuda-gdb 调试会话中解引用该位置以双检问题：

```
(cuda-gdb) print arr[tid]
Error: Failed to read global memory at 0x0 on device 0 sm 1 warp 0
(error)
(cuda-gdb)
```

显然这是无效的，这意味着 `arr` 的内容要么写入了无效值，要么没有被正确初始化。回看源代码，你应该注意到没有任何 `cudaMemcpy` 来填充数组 `d_matrix`。在内核启动之前添加以下行可以修复此错误。

```
cudaMemcpy(d_matrix, d_ptr, N * sizeof(int), cudaMemcpyHostToDevice);
```

可以从 wrox.com 下载修复后的 debug-segfault.fixed.cu。你仍然处于 cuda-gdb 调试会话中，你也可以检查 GPU 上其他线程的状态。使用 `cuda` 命令获取当前设备、块和线程，如下：

```
(cuda-gdb) cuda device block thread
block (0,0,0), thread (0,0,0), device 0
(cuda-gdb)
```

尝试切换到同一设备上的其他线程并检查不同的线程状态：

```
(cuda-gdb) cuda block 1 thread 1
Switching focus to CUDA kernel 1026, grid 107, block (1,0,0), thread (1,0,0),
device 0, sm 5, warp 0, lane 1
25
 arr[tid] = foo(tid, i);
(cuda-gdb) print tid
$2 = 257
(cuda-gdb) print arr[tid]
$3 = (@global int *@global) 0x0
(cuda-gdb)
```

显然许多线程都发生了内存错误。焦点只是被放在线程 ID 最小的线程上。

你可以通过输入 `y` 并回车来退出 cuda-gdb 会话：

```
(cuda-gdb) quit
A debugging session is active.
```

> Inferior 1 [process 11330] 将将被杀死。

 确定要退出吗？(y or n) y

# CUDA-GDB 总结

本节简要介绍了使用 cuda-gdb 调试工具检查内核执行。cuda-gdb 的用法与 gdb 几乎相同，因此你以前在主机调试工具上的任何经验都可以用于熟练调试 CUDA 应用程序。关于 cuda-gdb 的更多细节，鼓励你阅读 CUDA Toolkit 带的 CUDA-GDB 在线文档。

# CUDA printf

在调试期间，你可能在主机应用程序状态中常用 `printf`。如果可以在 GPU 设备代码中使用 `printf` 作为检查内部设备状态的简单方法，将太棒了。然而，在运行成千上万线程的设备内核上输出面临着挑战。从 CUDA 4.0 开始，NVIDIA 在设备上增加了 `printf` 支持。CUDA `printf` 的接口与你在主机上进行 C/C++ 开发时熟悉的接口相同（甚至需要相同的头文件 `stdio.h`），使得过渡到 CUDA `printf` 变得简单。

CUDA `printf` 有一些用用。它仅适用于计算能力为 2.0 或更高的设备。其次，除非你显式使用 CUDA 同步，否则线程之间没有打印顺序。一个固定大小的环形设备缓冲区用于临时存储内核的 `printf` 输出，然后将其获取到主机进行显示。结果是如果产生速度快于显示速度，缓冲区将回绕并覆盖旧内容。

