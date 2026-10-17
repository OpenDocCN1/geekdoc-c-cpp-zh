
- GPU 的 warp 大与预期的 32 线程 warp 不同。对于 x86 计算，warp 可能是 x86 核心上 SIMD 单元的大小（四或八），或者在未利用 SIMD 执行时每个 warp 一个线程。

- 在许多情况下，当发生同步调用时，PGI CUDA 编译器会移除显式同步。

> ⁶ http://drobs.com/high-performance-computing/207613.

# 第 8 章：适用于所有 GPU 和 CPU 应用的 CUDA

![](img/4468c911ce4bde7a6707b9c8097869_205_0.png)

**将 GPU 计算映射到 CPU**。

## NVIDIA NVCC 编译器

NVIDIA `nvcc` 编译器可以生成主机和设备内核。虽然这种方法非常有用，但需要 CUDA 程序员手动设置内存并妥善调用它。`Thrust` 还可以通过向 `nvcc` 传递额外的命令行选项，透明地为 x86 处理器等后端生成代码。

```bash
### Example 8.7
nvcc -o monte_carlo monte_carlo.cu -fopenmp -DTHRUST_DEVICE_BACKEND=OMP -lcudart -lgomp
```

## CUDA 到多个硬件后端的路径

| 表 8.1 使用 OpenMP 运行时的报告时间 | 秒 |

| :--- | :--- |

| GPU | 0.222 |

| 4 OpenMP 线程 | 2.090 |

| 2 OpenMP 线程 | 4.168 |

| 1 OpenMP 线程 | 8.333 |

`Thrust` 网站报告的时间显示是可以接受的（见表 8.1）。注意 `Thrust` 并没有针对产生最佳运行时进行优化。

### Ocelot

`Ocelot` 是一个流行且活跃维护的包。网站指出 `Ocelot` 可以在 NVIDIA GPU、AMD GPU 和 x86 处理器上全速运行 CUDA 二进制文件。它可以免费下载并根据 BSD 许可证授权。Gregory Damos 的论文《`Ocelot` 的 x86、从 PTX 到多核动态二进制翻译器》（2009）是他《GPU Computing Games》（Hwu, 2011）中的章节。

`Ocelot` 的核心能力包括：

- CUDA Runtime API 的实现。

- 结合控制流和数据流分析的 PTX 内核完整内部表示。

- PTX 的功能模拟器。

- 映射到高效执行的多核 x86 CPU 的 PTX 翻译器。

- 通过 CUDA 驱动程序到 NVIDIA GPU 的后端。

- 支持可扩展的跟踪生成框架，可以在指令级粒度观察应用程序行为。

`Ocelot` 有三个后端执行目标：

- PTX 模拟器。

- 从 PTX 到多核指令的翻译器。

- 支持 CUDA 的 GPU。

`Ocelot` 已针对来自 CUDA SDK、UIUC Parboi 基准测试、Virginia Rodinia 基准测试（Che 等，2009）、GPU-VSIPL 图像处理库、`thrust` 库以及多个领域特定应用的 130 应用程序进行了验证。它是分析和分析 CUDA 行为的典型工具，也可以作为 CUDA 可移植性的平台。

> 7 http://code.google.com/p/gpuocelot/

> 8 http://gpu-vspl.tri.gatech.edu/

### Swan

`Swan` 是一个免费的源到源翻译工具，可以将现有的 CUDA 代码转换为 OpenCL 模型。注意，转换过程需要人工干预，不是自动的。

作者报告说，移植到 OpenCL 的 CUDA 应用的运行速度慢约 50%（Harvey & Freitas, 2010）。作者将性能下降归因于 OpenCL 编译器的不成熟。

不清楚 `Swan` 项目是否仍在开发，最后更新是 2010 年 12 月。`Swan` 目前的版本不支持：

- 内核代码中的 CUDA C++ 模板。

- OpenCL /采样器（类似于纹理）——软件纹理插值。

- 单进程中的多设备管理。

- 为 CPU 编译内核。

- CUDA 设备模拟模式。

### SWIG

`SWIG`（简化封装和接口生成器）是一种软件开发工具，用于将用 C 和 C++ 编写的程序（包括 CUDA C/C++ 应用）与多种高级编程语言连接。`SWIG` 得到积极支持并广泛使用。你可以从 `SWIG` 网站免费下载.^9

根据目前的 2.0.4 版本，`SWIG` 为以下语言生成接口：

- AllegroCL

- C# – Mono

- C# – MS.NET

- CFFI

- CHICKEN

- CLISP

- D

- Go 语言

- Guile

- Java

- Lua

- MzScheme/Racket

- Ocaml

- Octave

- Perl

- PHP

- Python

- R

- Tcl/Tk

我在 *Doctor Dobb's Journal* 上的“面向大众的超级计算”教程系列中的第 9 部分^10 提供了一个完整的工作示例，使用 `SWIG` 将 CUDA 矩阵操作与 Python 建立接口。该示例也可以与其他语言建立接口（Farber, 2008）。

### Copperhead

`Copperhead` 是一个早期研究项目，旨在为 Python 语言引入数据并行性。它定义了 Python 的一个小型数据并行子集，该子集被动态编译运行在并行平台上。目前，NVIDIA GPU 是唯一的并行后端。

> ^9 http://swig.org.

^10 http://drdobobs.com/high-performance-computing/211800683.

示例 8.8，“Copperhead Python 代码示例”是 Copperhead 网站上的一个简单示例：

### 示例 8.8

```cpp
from copperhead import *
import numpy as np

@cu
def axpy(a, x, y):
    return [a*xi + yi for xi, yi in zip(x, y)]

x = np.arange(100, dtype=np.float64)
y = np.arange(100, dtype=np.float64)
with places.gpu0:
    gpu = axpy(2.0, x, y)
with places.here:
    cpu = axpy(2.0, x, y)
```

`Copperhead` 数据并行数组组织计算。在这个示例中，`Copperhead` 运行时拦截了对 `axpy()` 的调用，并将函数编译为 CUDA。运行时转换了由运行时管理的并行数组 CuRArrays 的执行。

程序员使用上一个示例所示的结构来指定执行位置。数据在执行位置之间进行懒性拷贝（lazy copy）。`Copperhead` 目前支持 GPU 执行和 Python 解释器执行。使用 Python 解释器用于算法原型设计。

### EXCEL

Microsoft Excel 是一种广泛采用的商业电子表格应用程序，由 Microsoft 为 Windows 和 Mac OS 编写并发布。它具有计算、图表工具以及许多其他工具。可以使用 Visual Basic 进行编程。NVIDIA 在其网站上分发了“Excel 2010 CUDA 集成示例”11，展示了如何在 Excel 中使用 CUDA。该 SDK 示例未包含在标准 SDK 中。

### MATLAB

`MATLAB` 是由 MathWorks 开发的商业应用。`MATLAB` 允许矩阵操作、函数和数据的绘图以及丰富的其他功能。开发者可以实现算法和用户界面，并将 `MATLAB` 集成到其他应用程序中。

> 11 http://developer.nvidia.com/cuda-cc-sdk-code-samples.

`MATLAB` GPU 支持可在并行计算工具箱（Parallel Computing Toolbox）中获得。它支持计算能力 1.3 及以上的 NVIDIA CUDA 启用 GPU。第三方产品（如 Accelereyes 的）提供了 `MATLAB` 对 GPU 计算的访问以及 CUDA 的矩阵库。^{12}

### 库

使用优化库通常是提高应用程序性能的简单方法。在迁移大型遗留项目时，库可能是针对新平台优化的唯一真实方法，因为代码更改需要大量的验证工作。本质上，库既方便又可以加速代码开发以及应用程序性能，但不能盲目地利用。特别是基于 GPU 的库，要求开发者仔细考虑数据放置以及库的使用方式，否则会导致性能低下的和过度的内存消耗。

### CUBLAS

基础线性代数程序（BLAS）包是向量和矩阵乘法等基础线性代数操作的事实接口。NVIDIA 使用其专为 GPU 设计的库 `CUBLAS` 支持此接口。应用程序使用 `CUBLAS` 库的基本模型是在 GPU 内存空间中创建向量和矩阵对象，用数据填充这些对象，调用系列 `CUBLAS` 函数，并将结果返回主机（host）。

`CUBLAS` 提供了辅助函数，用于在 GPU 空间中创建和销毁对象以及利用这些对象。CUDA 程序员应该注意，`CUBLAS` 为了最大程度兼容 FORTRAN，使用了列存储和从 1 开始的索引。C 和 C++ 应用程序需要使用宏或内联函数来方便访问由 `CUBLAS` 创建的对象。

第 1 章讨论了 BLAS 运行时级别以及最小化或消除数据移动的重要性。可以从 NVIDIA 网站下载的 `simpleBLAS` 示例提供了关于如何使用 `CUBLAS` 的基本演示。^{13}

### CUFFT

`CUFFT` 是另一个 NVIDIA 支持的库，提供了基于 GPU 的 FFT（快速傅里叶变换）实现，这是信号处理应用中常用的方法。`CUFFT` 效仿 `FFTW`，`FFTW` 是一种针对通用处理器的高度优化且流行的 FFT 包。

$^{12}$ http://www.accelereyes.com/

$^{13}$ http://www.nvidia.com/object/cuda_sample_linear_algebra.html.

`CUFFT` 利用计划（plan），这是一种简单的配置机制，根据给定的问题规模、数据类型和目标硬件平台，为特定算法指定最佳执行“计划”。这种方法的优势是，一旦创建了计划，它就可以应用程序的剩余生命周期内一直使用。这是库和其他高性能可移植代码中执行运行时配置的常用编程模式。NVIDIA 库使用这种配置模型，是因为不同尺寸和类型的 FFT 需要不同的配置和 GPU 资源。`simpleCUFFT` 示例可以从 NVIDIA 网站下载.^14 它涵盖了使用 `CUFFT` 库的基础知识。

`CUFFT` 还提供了 `cufftPlanMany()` 方法，它可以创建一个运行多个 FFT 操作的计划。这既是福音，也是内存大户。

测试程序演示了在单个或多个 GPU 上使用 `CUFFT`。它执行 3D 复数到复数的正向和反向原地变换，并计算这些变换引入的误差。正确的使用将产生小的误差。

用户可以通过命令行指定以下运行时特性：

- 使用的 GPU 数量。这必须小于或等于 GPU 的总数。

- 每个维度的大小。

- 要执行的 FFT 总数。

- 可选值，指定每次调用执行多少 FFT。

由 GPU 创建。指向设备内存的指针存储在 vector `d_data.data` 中。参见示例 8.11，“fft3D.cu 的第 3 部分”：

### 示例 8.11

```cpp
public:
    DistFFT3D(int nGPU, Real* _h_data, long _h_data_elements,
        int *_dim, int nPerCall, cudaStream_t* _streams) {
        nGPU = _nGPU;
        h_data = _h_data;
        h_data_elements = _h_data_elements;
        dim[0]=_dim[0]; dim[1]=_dim[1]; dim[2]=_dim[2];
        nfft[0]=2*dim[1]*dim[2];
        nfft3d=2*dim[0]*dim[1]*dim[2];
        totalFFT=h_data_elements/nfft3d;

        setPerCall(nPerCall);
        bytesPerGPU = nPerCall*nfft3d*sizeof(Real);
        h_memsize = h_data_elements*sizeof(Real);
        assert((totalFFT/nPerCall*bytesPerGPU) == h_memsize);

        streams = _streams;
        fftPlanMany = vector<cufftHandle>(nGPU);

        initFFTs();

        for(int i=0; i<nGPU; i++) {
            Real tmp;
            cudaSetDevice(i);
            if(cudaMalloc(&tmp,bytesPerGPU)) {
                cerr << "Cannot allocate space on device!" << endl;
                exit(1);
            }
            d_data.push_back(tmp);
        }
    }

    void setPerCall(int n) {
        cerr << "Setting nPerCall *" << n << endl;
        nPerCall = n;
        if((nGPU * nPerCall) > totalFFT) {
            cerr << "Too many nPerCall specified! max " << (totalFFT/nGPU) << endl;
            exit(1);
        }
    }
```

析构函数释放了示例 8.12，“fft3Dtest.cu 的第 4 部分”中在设备上分配的数据：

```cpp
Example 8.12
~DistFFT3D() {
    for(int i=0; i<nGPU; i++){
      cudaSetDevice(i);
      cudaFree(d_data[i]);
    }
}
```

示例 8.13，“fft3Dtest.cu 的第 5 部分”初始化多计划 FFT，并提供了为 float 和 double 变量类型正确调用 CUFF 方法的模板。注意使用 `cuftSetStream()` 设置流：

```cpp
Example 8.13
void inline initFFTs() {
    if((nPerCall*nGPU) > totalFFT) {
      cerr << "nPerCall must be a multiple of totalFFT" << endl;
      exit(1);
    }
    // 创建批处理 3D 计划
    for(int sid=0; sid<nGPU; sid++) {
      cudaSetDevice(sid);
      if(sizeof(Real) == sizeof(float)) {
            cuffPlanFFPlanMany(&fftPlanMany[sid], 3, dim, NULL, 1, 0, NULL, 1, 0,
            CUFFT_C2C,nPerCall);
      } else {
            cuffPlanPlanMany(&fftPlanMany[sid], 3, dim, NULL, 1, 0, NULL, 1, 0,
            CUFFT_Z2Z,nPerCall);
      }
      if(cuftSetStream(fftPlanMany[sid],streams[sid])) {
        cerr << "cuftSetStream failed!" << endl;
      }
    }
    cudaSetDevice(0);
}
```

```cpp
inline void _FFError(int ret) {
    switch(ret) {
    case CUFFT_SETUP_FAILED: cerr << "SETUP_FAILED" << endl; break;
    case CUFFT_INVALID_PLAN: cerr << "INVALID_PLAN" << endl; break;
    case CUFFT_INVALID_VALUE: cerr << "INVALID_VALUE" << endl; break;
    case CUFFT_EXEC_FAILED: cerr << "EXEC_FAILED" << endl; break;
    default: cerr << "UNKNOWN ret code" << ret << endl;
    }
}
```

# 第 8 章：适用于所有 GPU 和 CPU 程序的 CUDA
