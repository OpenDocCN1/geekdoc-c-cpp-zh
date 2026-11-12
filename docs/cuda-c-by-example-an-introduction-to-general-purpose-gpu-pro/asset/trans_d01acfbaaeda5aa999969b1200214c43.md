

该类使用两个数据元素表示复数：一个单精度实部 r 和一个单精度虚部 i。该类定义了加法和乘法运算符，用于按预期组合复数。（如果你对复数完全陌生，可以在网上快速了解相关知识。）最后，我们定义一个返回复数模值的方法。

## GPU 朱利亚集

设备实现与 CPU 版本非常相似，延续了你可能已经注意到的趋势。

```cpp
int main( void ) {
    CPUBitmap bitmap( DIM, DIM ) ;
    unsigned char *dev_bitmap;
    HANDLE_ERROR( cudaMalloc( (void**)&dev_bitmap,
                              bitmap.image_size() ) );
    dim3 grid(DIM,DIM);
    kernel<<<grid,1>>>( dev_bitmap );
    HANDLE_ERROR( cudaMemcpy( bitmap.get_ptr(),
                              dev_bitmap,
                              bitmap.image_size(),
                              cudaMemcpyDeviceToHost ) );
    bitmap.display_and_exit();
    cudaFree( dev_bitmap );
}
```

这个 main() 版本看起来比 CPU 版本复杂得多，但实际流程是相同的。与 CPU 版本一样，我们使用实用库创建一个 DIM × DIM 位图图像。但由于我们将在 GPU 上进行计算，我们还声明了一个名为 `dev_bitmap` 的指针，用于保存设备上数据的副本。并且为了存储数据，我们需要使用 `cudaMalloc()` 分配内存。

然后我们像 CPU 版本一样运行 `kernel()` 函数，只不过现在它是一个 `__global__` 函数，意味着它将在 GPU 上运行。与 CPU 示例一样，我们将上一行分配的指针传递给 `kernel()` 以存储结果。唯一的区别是，内存现在位于 GPU 上，而不是主机系统上。

最显著的区别在于，我们指定了要执行函数 `kernel()` 的并行块数量。由于每个点都可以独立于其他点进行计算，我们只需为要计算的每个点指定一个函数副本。我们提到，对于某些问题领域，使用二维索引很有帮助。不出所料，在复平面等二维域上计算函数值就是这类问题之一。因此，我们在这一行中指定了一个二维块网格：

```cpp
dim3 grid(DIM,DIM);
```

类型 `dim3` 不是标准 C 类型，请别担心你漏掉了什么关键信息。相反，CUDA 运行时头文件定义了一些便利类型，用于封装多维元组。类型 `dim3` 表示一个三维元组，用于指定我们的启动大小。但是，当我们明明清楚地声明启动是一个 *二维网格* 时，为什么还要使用三维值呢？

坦率地说，我们这样做是因为 CUDA 运行时期望一个三维的 `dim3` 值。虽然目前不支持三维启动网格，但 CUDA 运行时仍然期望一个 `dim3` 变量，其最后一个分量等于 1。当我们只用两个值初始化它时，就像在语句 `dim3 grid(DIM, DIM)` 中所做的那样，CUDA 运行时会自动将第三个维度填充为值 1，因此这里一切都会按预期工作。虽然 NVIDIA 未来可能会支持三维网格，但目前我们将友好地与内核启动 API 打交道，因为当程序员和 API 发生冲突时，API 始终获胜。

然后我们在这一行中将 dim3 变量 grid 传递给 CUDA 运行时：

```cpp
kernel<<<grid,1>>>( dev_bitmap );
```

最后，由于结果位于设备上，执行 kernel() 后，我们必须将结果复制回主机。正如我们在前面章节中学到的，我们通过调用 cudaMemcpy() 来完成此操作，将方向 cudaMemcpyDeviceToHost 指定为最后一个参数。

```cpp
HANDLE_ERROR( cudaMemcpy( bitmap.get_ptr(),
                              dev_bitmap,
                              bitmap.image_size(),
                              cudaMemcpyDeviceToHost ) );
```

实现差异中的最后一个细节之一出现在 kernel() 的实现中。

```cpp
__global__ void kernel( unsigned char *ptr ) {
    // map from threadIdx/BlockIdx to pixel position
    int x = blockIdx.x;
    int y = blockIdx.y;
    int offset = x + y * gridDim.x;

    // now calculate the value at that position
    int juliaValue = julia( x, y );
    ptr[offset*4 + 0] = 255 * juliaValue;
    ptr[offset*4 + 1] = 0;
    ptr[offset*4 + 2] = 0;
    ptr[offset*4 + 3] = 255;
}
```

首先，我们需要将 kernel() 声明为 __global__ 函数，以便它在设备上运行但可以从主机调用。与 CPU 版本不同，我们不再需要嵌套的 for() 循环来生成传递给 julia() 的像素索引。与向量加法示例一样，CUDA 运行时在变量 blockIdx 中为我们生成这些索引。之所以有效，是因为我们声明的块网格与图像具有相同的维度，因此我们在 (0,0) 到 (DIM-1, DIM-1) 之间的每个整数对 (x,y) 都会得到一个块。

接下来，我们需要的唯一额外信息是输出缓冲区 ptr 中的线性偏移量。这是使用另一个内置变量 gridDim 计算的。该变量在所有块中都是常量，仅保存启动的网格维度。在此示例中，它始终是值 (DIM, DIM)。因此，将行索引乘以网格宽度并加上列索引，将给出 ptr 中一个唯一的索引，范围从 0 到 (DIM*DIM-1)。

```cpp
int offset = x + y * gridDim.x;
```

最后，我们来看看决定一个点是否在朱利亚集内或外的实际代码。这段代码应该与 CPU 版本相同，延续了我们在许多示例中看到的趋势。

```cpp
__device__ int julia( int x, int y ) {
    const float scale = 1.5;
    float jx = scale * (float) (DIM/2 - x) / (DIM/2) ;
    float jy = scale * (float) (DIM/2 - y) / (DIM/2) ;

    cuComplex c(-0.8, 0.156);
    cuComplex a(jx, jy);

    int i = 0;
    for (i=0; i<200; i++) {
        a = a * a + c;
        if (a.magnitude2() > 1000)
            return 0;
    }

    return 1;
}
```

再次，我们定义一个 cuComplex 结构体，用于定义存储带有单精度浮点分量的复数的方法。该结构体还定义了加法和乘法运算符，以及一个返回复数值模值的函数。

```cpp
struct cuComplex {
    float r;
    float i;
    cuComplex( float a, float b ) : r(a), i(b) {}
    __device__ float magnitude2( void ) {
        return r * r + i * i;
    }
    __device__ cuComplex operator*(const cuComplex& a) {
        return cuComplex(r*a.r - i*a.i, i*a.r + r*a.i);
    }
    __device__ cuComplex operator+(const cuComplex& a) {
        return cuComplex(r+a.r, i+a.i);
    }
};
```

请注意，我们在 CUDA C 中使用的语言结构与 CPU 版本中使用的相同。唯一的区别是限定符 __device__，它表示这段代码将在 GPU 上运行而不是在主机上。请回顾，由于这些函数被声明为 __device__ 函数，它们只能从其他 __device__ 函数或 __global__ 函数中调用。

由于我们频繁地用注释中断代码，以下是从头到尾的完整源代码清单：

```cpp
#include "../common/book.h"
#include "../common/cpu_bitmap.h"
#define DIM 1000

struct cuComplex {
    float r;
    float i;
    cuComplex( float a, float b ) : r(a), i(b) {}
    __device__ float magnitude2( void ) {
        return r * r + i * i;
    }
    __device__ cuComplex operator*(const cuComplex& a) {
        return cuComplex(r*a.r - i*a.i, i*a.r + r*a.i);
    }
    __device__ cuComplex operator+(const cuComplex& a) {
        return cuComplex(r+a.r, i+a.i);
    }
};

__device__ int julia( int x, int y ) {
    const float scale = 1.5;
    float jx = scale * (float)(DIM/2 - x)/(DIM/2);
    float jy = scale * (float)(DIM/2 - y)/(DIM/2);

    cuComplex c(-0.8, 0.156);
    cuComplex a(jx, jy);

    int i = 0;
    for (i=0; i<200; i++) {
        a = a * a + c;
        if (a.magnitude2() > 1000)
            return 0;
    }
    return 1;
}
```

