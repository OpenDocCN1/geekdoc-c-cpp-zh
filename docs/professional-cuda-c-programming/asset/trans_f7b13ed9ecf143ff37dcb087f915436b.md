
你可能已经注意到网格大小（grid size）向上取整到块大小（block size）的倍数。你将在下一章学习到必须这样计算网格大小的原因。下面的代码段将显示网格检查和块维度：

```c
printf("grid.x %d grid.y %d grid.z %d\n", grid.x, grid.y, grid.z);
printf("block.x %d block.y %d block.z %d\n", block.x, block.y, block.z);
```

在内核函数中，每个线程按照如下方式打印其线程索引、块索引和网格维度：

```c
printf("threadIdx:(%d, %d, %d) blockIdx:(%d, %d, %d) blockDim:(%d, %d, %d) \ngridDim:(%d, %d, %d)\n", threadIdx.x, threadIdx.y, threadIdx.z,
blockIdx.x, blockIdx.y, blockIdx.z, blockDim.x, blockDim.y, blockDim.z,
gridDim.x, gridDim.y, gridDim.z);
```

你将代码线程组合到一个名为 `checkDimension.cu` 的文件中，如列表 2-2 所示。

##  2-2：检查网格和块索引 (checkDimension.cu)

```c
#include <cuda_runtime.h>
#include <stdio.h>

__global void checkIndex(void) {
    printf("threadIdx:(%d, %d, %d) blockIdx:(%d, %d, %d) blockDim:(%d, %d, %d) \ngridDim:(%d, %d, %d)\n", threadIdx.x, threadIdx.y, threadIdx.z,
blockIdx.x, blockIdx.y, blockIdx.z, blockDim.x, blockDim.y, blockDim.z,
gridDim.x, gridDim.y, gridDim.z);
}

int main(int argc, char **argv) {
    // 定义总数据元素
    int nElem = 6;

    // 定义网格和块结构
    dim3 block(3);
    dim3 grid((nElem+block.x-1)/block.x);

    // 从主机端检查网格和块维度
    printf("grid.x %d grid.y %d grid.z %d\n", grid.x, grid.y, grid.z);
    printf("block.x %d block.y %d block.z %d\n", block.x, block.y, block.z);

    // 从设备端检查块维度
    checkIndex<<<grid, block>>();

    // 离开前重置设备
    cudaDeviceReset();

    return(0);
}
```

现在你准备好编译并运行这个示例了：

```bash
$ nvcc -arch=sm_20 checkDimension.cu -o check
$ ./check
```

由于 `printf` 函数仅支持从 Fermi GPU 开始的架构，因此必须添加 `-arch=sm_20` 编译器选项。默认情况下，`nvcc` 会为最低 GPU 架构生成代码。该应用程序的结果所示。你可以看到每个线程都有自己的坐标，并且所有线程具有相同的块维度和网格维度。

```
grid.x 2 grid.y 1 grid.z 1
block.x 3 block.y 1 block.z 1
threadIdx:(0, 0, 0) blockDim:(1, 0, 0) blockDim:(3, 1, 1) gridDim:(2, 1, 1)
threadIdx:(1, 0, 0) blockDim:(1, 0, 0) blockDim:(3, 1, 1) gridDim:(2, 1, 1)
threadIdx:(2, 0, 0) blockDim:(1, 0, 0) blockDim:(3, 1, 1) gridDim:(2, 1, 1)
threadIdx:(0, 0, 0) blockDim:(0, 0, 0) blockDim:(3, 1, 1) gridDim:(2, 1, 1)
threadIdx:(1, 0, 0) blockDim:(0, 0, 0) blockDim:(3, 1, 1) gridDim:(2, 1, 1)
threadIdx:(2, 0, 0) blockDim:(0, 0, 0) blockDim:(3, 1, 1) gridDim:(2, 1, 1)
```

## 从主机端和设备端访问网格/变量

区分主机端和设备端对网格和块变量的访问是非常重要的。例如，从主机端使用一个声明为块的变量，你按照如下方式定义坐标并访问它们：

```
block.x, block.y, 和 block.z
```

在设备端，你有一个预初始化的内置块大小变量可用：`blockDim.x`、`blockDim.y` 和 `blockDim.z`。

总而言之，你在启动内核之前在主机上定义网格和块的变量，并通过主机端向量结构的 `x`、`y` 和 `z` 字段访问它们。当内核启动时，你可以在内核可以使用预初始化的内置变量。

对于给定的数据大小，确定网格和块维度的通用步骤是：

- 决定块大小。
- 根据应用程序数据大小和块大小计算网格维度。

确定块维度通常需要考虑：

- 内核的性能特性。
- GPU 资源的限制。

你将在书中后续章节示例中学习更多关于这些因素的细节。列表 2-3 使用 1D 网格和 1D 块来说当块大小改变时，网格大小将随之变化。

## 2-3：在主机上定义网格和块维度 (defineGridBlock.cu)

```c
#include <cuda_runtime.h>
#include <stdio.h>

int main(int argc, char **argv) {
    // 定义总数据元素
    int nElement = 1024;

    // 定义网格和块结构
    dim3 block;
    dim3 grid = (nElement+block.x-1)/block.x;
    printf("grid %d block.x %d \n",grid.x, block.x);

    // 重置块
    block.x = 3;
    printf("grid %d block.x %d \n",grid.x, block.x);

    // 从设备端检查块维度
    checkIndex<<<grid, block>>();

    // 离开前重置设备
    cudaDeviceReset();

    return(0);
}
```
（注：第 62-64 页的剩余文本高度重复/损坏；我已合并了上述提供的唯一内容段。）
