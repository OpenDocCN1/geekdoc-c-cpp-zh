
```
/* SCALAR SAXPY */
void saxpy(int n, float a, float* x, float* y)
{
    // n is the number of float elements
    for (int i=0; i<n; i++)    y[i] = a*x[i] + y[i];
}

/* OpenVec SIMD SAXPY */
void vsaxpy(int n, float a, ov_float* x, ov_float* y)
{
    // nv is the number of SIMD elements
    int const nv = (n-1)/OV_FLOAT_WIDTH + 1;
    for (int i=0; i<nv; i++) y[i] = a*x[i] + y[i];
}

## 图24.2

标量SAXPY与OpenVec SIMD SAXPY。

“d，”例如 ov_alld。在Intel SSE、ARM Neon和IBM Altivec上，由于没有支持双精度浮点的向量指令，双精度运算通过标量后端实现。在这些平台上，OV_DOUBLE_WIDTH 将为1。切勿假设 OV_DOUBLE_WIDTH 与 OV_FLOAT_WIDTH 具有相同的值。

## 向量类型

为了避免开销，所有实现都包含在OpenVec头文件中。要启用OpenVec，开发者必须包含“openvec.h”。该头文件将OpenVec可移植内建函数映射到厂商专有的向量内建函数。如果语言是C++，它还会创建适当的算术运算符定义。

OpenVec向量类型 ov_float 创建 OV_FLOAT_WIDTH 个浮点数的实例，你可以像声明普通浮点数一样声明它。例如，在ARM Neon、IBM Altivec和Intel SSE中，OV_FLOAT_WIDTH=4，每个 ov_float 变量包含四个浮点数；在Intel IMCI和AVX-512中，OV_FLOAT_WIDTH=16；因此，ov_float 变量包含多个浮点元素，所有操作都会作用于所有元素。

编译时常量 OV_FLOAT_WIDTH 表示浮点数的SIMD宽度，并为每种架构定义为每个 ov_float 类型的浮点数数量。在标量后端，OV_FLOAT_WIDTH=1，ov_float 被定义为 float 类型。

ov_free 释放由 ov_malloc/ov_calloc 分配的内存。由 ov_malloc/ov_calloc 分配的内存必须由 ov_free 释放。

我们目前的实现使用 posix_memalign 在 ov_malloc 函数内部。提供了编译时常量 OV_ALIGN，它包含以字节为单位的对齐大小，同时 ov_malloc 分配 size+OV_ALIGN，从而无需处理向量尾部，这将在后面讨论。

当分配对齐内存时，首元素的地址是对齐的（即与 array[0] 的地址对齐），所有索引为 OV_FLOAT_WIDTH 的倍数的元素将位于对齐地址（即如果 index 模 OV_FLOAT_WIDTH = 0，则 array[index] 对齐）。有不同内建函数用于访问对齐和非对齐地址；通常，访问非对齐地址会产生性能损失。接下来，我们将介绍这些内建函数。

## 内建函数

OpenVec 提供了一些基本的内建函数；其中大多数直接映射到SIMD硬件指令。所有内建函数都已在所有支持的架构上测试过。这些函数将其行为应用于向量类型的所有元素。例如：ov_sqrtf(x) 将计算 x 的所有浮点元素的平方根。图24.4显示了提供的可移植内建函数。

ov_stream_stf 和 ov_nt_storef 流式存储内建函数在一些支持它们的架构上会带来性能提升。在不支持的架构上，它们将映射为常规的对齐存储 ov_stf。

例如，ov_maddf 内建函数在 AVX-512 上映射为 _mm512_fmadd_ps，在 ARM NEON 上映射为 vmla q_f32，在 SSE 上映射为 _mm_mul_ps 和 _mm_add_ps 的组合。

这些内建函数非常容易理解，除了加载/存储（LD/ST）内建函数。在C/C++代码中，这些操作通常是隐式的。借助OpenVec，我们可以使用隐式或显式的LD/ST。图24.5使用BLAS saxpy来演示隐式和显式的LD/ST。

该示例假设数据是对齐的，因为循环从索引0开始，每一步跳转 OV_FLOAT_WIDTH，所以所有索引都将对齐，因为对于所有步骤：

```
i MOD OV_FLOAT_WIDTH = 0
```

但如果无法安全假设对齐，则应使用加载和存储的非对齐版本，添加前缀“u”，如 ov_udf 和 ov_ustf。如果数据未对齐，不要使用隐式表示法。

像 + 和 - 这样的数学运算符符号在C++中已定义，但在纯C中，开发者必须使用内建函数进行基本数学运算，例如，c = a + b 在C中应写成 c = ov_addf(a,b)。

```
ov_float a,b,c;
// C++ code with implicit call to ov_addf intrinsic
c = a + b;
/* equivalent C code with explicit call */
c = ov_addf(a,b);
```

考虑到C代码的这一限制，C++代码比纯C代码更易读、更易维护。值得注意的是，我们观察到使用纯C带来了一些性能提升，性能数据将在本章后面给出。OpenVec的C实现真正实现了零开销，因为它仅通过预处理器宏映射内建函数。

通过将OpenVec内建函数映射到新架构，并基于先前架构创建新的头文件，可以轻松添加新架构。例如，ARM NEON 的 ov_float

## 470 第24章 可移植显式向量化内建函数

| 内建函数 | 操作/描述 |
|---|---|
| `ov_addf(x, y)` | `x + y` |
| `ov_subf(x, y)` | `x - y` |
| `ov_mulf(x, y)` | `x * y` |
| `ov_divf(x, y)` | `x / y` |
| `ov_ldf(address)` | 从对齐地址加载向量 |
| `ov_uldf(address)` | 从非对齐地址加载向量 |
| `ov_stf(address, x)` | 将向量 x 存储到对齐地址 |
| `ov_storeu(address, x)` | 将向量 x 存储到非对齐地址 |
| `ov_stream_stf(address, x)` | 流式存储向量 x 到对齐地址 |
| `ov_nt_storef(address, x)` | 非时态存储向量 x 到对齐地址 |
| `ov_setzerof(x)` | 将 x 的所有值设为0 |
| `ov_getzerof()` | 返回一个零值向量 |
| `ov_setf(scalar)` | 创建一个所有元素都等于标量的向量 |
| `ov_maxf(x, y)` | 返回逐元素最大值 |
| `ov_minf(x, y)` | 返回逐元素最小值 |
| `ov_rsqrtf(x)` | 倒数平方根；`1/sqrt(x)` |
| `ov_sqrtf(x)` | 平方根 |
| `ov_sqrf(x)` | `x * x` |
| `ov_rcpf(x)` | 倒数 `1/x` |
| `ov_floorf(x)` | 向下取整 |
| `ov_ceilf(x)` | 向上取整 |
| `ov_maddf(x, y, z)` | `(x*y) + z` |
| `ov_msubf(x, y, z)` | `(x*y) - z` |
| `ov_absf(x)` | 绝对值 |

**图24.4**  
OpenVec 可移植内建函数。存在后缀为 d 的等效双精度版本，例如 `ov_maddd`。

```
void vsaxpy(int n, float a, ov_float* x, ov_float* y)
{
    int const nv = (n-1)/OV_FLOAT_WIDTH + 1;
    for (int i=0; i<nv; i++)
        y[i] = a*x[i] + y[i]; // Implicit LD/ST
}
```

```
void vsaxpy(int n, float a, float* x, float* y)
{
    // Where n is the number of floats
    // Jump to next vector address: +OV_FLOAT_WIDTH
    for (int i=0; i<n; i+=OV_FLOAT_WIDTH)
    {
        ov_float vy = ov_ldf(&y[i]); // Explicit LOAD
        ov_float vx = ov_ldf(&x[i]); // Explicit LOAD
        vy = a*vx + vy;
        ov_stf(&y[i], vy); // Explicit store
    }
}
```

## 图24.5

隐式和显式的加载/存储。

向量类型将被定义为 `float32x4_t`，而在 Intel AVX 上，该类型将为 `__m256`。为了让你了解实现的简洁性，AVX头文件只需不到一百行代码即可定义单精度实现。该项目的目标之一是轻松添加新架构和自定义。

高级用户可以根据自己的应用和精度需求修改或创建新平台，同时保持代码的可移植性。例如，ARM NEON没有原生的SIMD除法，因此可以将除法定义为：

```
#define ov_div(x,y) ov_mulf(x, ov_rcpf(y)) // x * (1/y)
```

这比ARM NEON提供的版本可能更快，但精度稍低。请注意，正如该示例所示，用户可以根据不同精度需求自定义OpenVec。

## IF/ELSE 向量化

SIMD架构的主要概念是在向量的所有元素上执行同一条指令，但如果出现由if/else语句导致的分支路径，会发生什么？不幸的是，同一条指令必须应用于向量类型的所有元素。对发散代码进行向量化的方法是同时执行if和else块，然后根据每个元素的代码路径合并两次执行结果。以下是对if/else进行向量化的常用技巧：

- 获取一个比特掩码，对评估为真的元素置1，这些元素应进入if代码块；
- 将掩码应用于if代码块的结果，通常是按位与；
- 将反向掩码应用于else代码块的结果；
- 合并两个掩码结果，通常是按位或；

下面是一个简单的if/else代码：

```
for (int i =0; i <n; i++){
    if (x[i] >y[i]) scalar_result[i] =x[i]-y[i];
    else scalar_result[i] =y[i] +x[i];
```

图24.6显示了OpenVec掩码SIMD版本：

从图24.6的代码中可以看到，ov_conditionalf 函数隐藏了掩码合并的几个复杂步骤：图24.7显示了Intel SSE的等效代码。

图24.6中的示例使用C++的“>”运算符进行大于比较；在C中，必须使用 ov_gtf(x,y) 函数，它表示浮点数大于。它返回一个掩码，在 x > y 的位置位设置为1。以下是此功能的所有变体：

```
for (int i=0; i<n; i+=OV_FLOAT_WIDTH)
{
    ov_float const vx=ov_ldf(&x[i]); // Load x and y
    ov_float const vy=ov_ldf(&y[i]);
    /* Merge two vectors depending on
       a comparison expression */
    ov_float result;
    result = ov_conditionalf(vx > vy, vx-vy, vy+vx);
    ov_stf(&simd_result[i], result); // Store the results
}
```

## 图24.6

IF/ELSE 向量化。
