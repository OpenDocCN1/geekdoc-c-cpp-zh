

![](img/506ba3a4c9f4512233692f3f20de1f3a_44_0.png)

图 1-16

# 来自 GPU 的 HELLO WORLD

学习新编程语言的最佳方法是使用该新语言编写程序。在本节中，你将编写第一个运行在 GPU 上的内核代码（kernel code）。对于所有语言，第一个程序都是相同的：打印字符串“Hello World.”

如果这是你第一次使用 CUDA，你可能想在 Linux 系统上通过以下命令检查 CUDA 编译器是否已正确安装：

```bash
$ which nvcc
```

典型的响应如下：

```
/usr/local/cuda/bin/nvcc
```

你还需要检查机器中是否连接了 GPU 加速器。在 Linux 系统上，你可以通过以下命令进行检查：

```bash
$ ls -1 /dev/nv*
```

典型的响应如下：

```
crw-rw-rw- 1 root 195, 0 Jul 3 13:44 /dev/nvidia0
crw-rw-rw- 1 root 195, 1 Jul 3 13:44 /dev/nvidia1
crw-rw-rw- 1 root 195, 255 Jul 3 13:44 /dev/nvidiactl
crw-rw---- 1 root 190, 144 Jul 3 13:39 /dev/nvram0
```

在例例中，你安装了两个 GPU（你的配置可能不同，可能会显示更多或更少的设备）。现在你已经准备好编写第一个 CUDA C 程序了。要编写 CUDA C 程序，你需要：

- 1. 创建一个带有特殊扩展名 `.cu` 的源代码文件。
- 2. 使用 CUDA `nvcc` 编译器编译程序。
- 3. 从命令行运行可执行文件，该文件包含在 GPU 上执行的内核代码。

作为一个开始，编写如下所示的打印“Hello World”的 C 程序：

```c
#include <stdio.h>
int main(void)
{
    printf("Hello World from CPU!\n");
}
```

将代码保存为 `hello.cu`，然后用 `nvcc` 编译。CUDA `nvcc` 编译器的语义与 `gcc` 等其他编译器相似。

```bash
$ nvcc hello.cu -o hello
```

如果你运行可执行文件 `hello`，它将打印：

Hello World from CPU!

接下来，编写一个名为 `helloFromGPU` 的内核函数，按如下所示打印字符串“Hello World from GPU!”：

```c
__global__ void helloFromGPU(void)
{
    printf("Hello World from GPU!\n");
}
```

`__global__` 限定符告诉编译器该函数将从 CPU 调用并并在 GPU 上执行。使用 `<<<1,10>>>` 启动内核。

```c
helloFromGPU<<<1,10>>>();
```

三角括号标记了从主机（host）到设备端（device）代码的调用。内核由线程数组执行，所有线程都运行相同的内核。三角括号内的参数是执行配置，它指定了有多少线程将执行该内核。在本例中，你将运行 10 个 GPU 线程。将所有这些结合在一起，你就得到了列表 I-1 中的程序：

# 列表 1-1: Hello World from GPU (hello.cu)

```c
#include <stdio.h>
__global__ void helloFromGPU(void)
{
    printf("Hello World from GPU!\n");
}

int main(void)
{
  // hello from cpu
  printf("Hello World from CPU!\n");

  helloFromGPU<<<1, 10>>>();
  return 0;
}
```

