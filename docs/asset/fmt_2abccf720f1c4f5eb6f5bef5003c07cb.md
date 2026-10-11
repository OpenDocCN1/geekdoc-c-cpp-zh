
`let len11 = Array.Create(len)`

`len10.[0] <- 1.f`

`len11.[0] <- 0.f`

`[1..len]`

`|>` `Seq.map` `(fun i ->`

`if i % 2 = 1 then`

`let r = computePascal(len10, len11)`

`r`

`else`

`let r = computePascal(len11, len10)`

`r)`

`|>` `Seq.toList`

`|>` `ignore`

`stopwatch.Stop()`

`printf("%A" stopwatch.Elapsed)`

// 使用 GPU 版本运行 CPU 版本的结果

```
00:00.1034888
temp.cu
c:\mycode\codecenter\fsharpgpu\fsharpgpu\fbin\CUDALibrary.h(56): warning
: variable "sizeT" was declared but never referenced
```

```
temp.cu
tmpxt_00001558000000000-3_temp.cuda1.gpu
tmpxt_00001558000000000-10_temp.cuda2.gpu
```

![](img/63aaf94e22830ab98ce16c5946be8ef6_611_0.png)

**图 9-9** 来自 BOPM 的二项分布树

在前面的图中，你可以找到以下关系：

$A^{rowX}[i] = \begin{cases} A^{rowX-1}[i] \times u, & \text{当 } i = 0 \ A^{rowX-1}[i-1] \times d, & \text{当 } i \neq 0 \end{cases}$

你可以轻松地将杨斯三角函数更改为 BOPM，如列表 9-33 所示。

### 列表 9-33 BOPM 函数

```
let blockIdx = new BlockDim()
let threadIdx = new ThreadIdx()

[ReflectedDefinition; GPU]
let bop: (a:CUDAPointer<float32>) (b:CUDAPointer<float32>) =
let u = 0.2f
let d = 1.f / u

let x = blockIdx.x
if x = 0 then
    b.Set(a.[x] * u, x)
else
    b.Set(a.[x - 1] * d, x)
()
```

# 子数组中的最大值

处理数组是 GPU 可以提供帮助的场景之一。由于 GPU 拥有数十个处理器，它可以同时处理元素。在本节中，你需要找到数组中最大的元素。该函数接收数组和搜索起点，并返回从该起点开始的最大元素。

### 列表 9-34 在数组中寻找最大值

```
let blockIdx = new BlockDim()
let threadIdx = new ThreadIdx()

let input = [1.f .. 15.f] | Array.of

<ReflectedDefinition; GPU>
let sample4(a:CUDAPointer<float32>, b:CUDAPointer<float32>) : unit =
let x = blockIdx.x
let mutable max = 0.f
for i = x to 15 do
    if max < a.[i] then
        max -= a.[i]
    else
        ()
b.Set(max, x)

let WriteToFile2() =
let al = <<@sample4@@ // 定义在列表 9-28
let b = getCUDACode(al)
let commonCode = getCommonCode() // 定义在列表 9-28
System.IO.File.Delete(tempFileName) // 定义在列表 9-28
System.IO.File.WriteAllText(tempFileName, commonCode + b);

let getMax() =
let tempFileName = "@.temp.cu"
WriteToFile2()
let execution = new GPUExecution()
let m = execution.Init(tempFileName)
let output = Array.create("sample4", [input; output])
let r, ps = execution.Execute("sample4", [input; output])
let results =
let ps
| List.map(fun p -> p.ToArray() | snd)
()
```

```cpp
#include <CUDibrary.h>

__device__ void ff_0(float* a, float* b) { int x;
x = blockIdx.x;
float max;
max = 0.0F;
for (int i = x; i<15; i++) { if ((max) < (a[i])) max = a[i];
else
         };
b[x] = max;
}

extern "C"__global__ void sample4(float* a, float* b) {
}
}
}
```

# 使用蒙特卡洛模拟在 GPU 上计算 pi

除了使用 GPU 处理数组外，你还可以将它们用于模拟。在本节中，你将查看使用蒙特卡洛模拟计算 $\pi$ 的小型应用。该算法用于计算区域中的随机命中。两个区域是一个正方形和一个触及正方形边缘的圆。如果你知道圆的半径是 $r$，那么圆的面积是 $\pi r^2$，而正方形的面积是 $4r^2$。想象区域中有大量的随机命中。$\pi$ 值可以通过圆区域的命中次数和矩形区域的命中次数计算出来。

![](img/63aaf94e22830ab98ce16c5946be8ef6_13_0.png)

图 9-10 蒙特卡洛模拟中的圆和矩形

`cuRand` 库提供了生成 0 到 1 之间数字的函数。如图 9-10 所示，你可以创建一个涉及 $\pi$ 计算的圆。从 `area1` 和 `area2` 计算 $\pi$ 值的公式如下：

```
$\frac{1}{4}\pi r^2 = \frac{\text{hit in area0}}{\text{hit in area1}}$
$\frac{\pi}{4} = \frac{\text{hit in area0}}{\text{hit in area1}}$
$\pi = \frac{\text{hit in area0}}{\text{hit in area1}} \times 4$
```

![](img/63aaf94e22830ab98ce16c5946be8ef6_14_0.png)

图 9-11 使用 cuRand 库进行 蒙特卡洛计算

在生成代码之前，列表 9-35 中的翻译用于转换 `sqrt` 函数。然后需要将代码添加到列表 9-20 所示的 `translateFrom` 函数中。

### 列表 9-35 翻译 sqrt 函数

```
"Sqrt" ->
GPU 代码定义在列表 9.36 的 `sample` 函数中。`WriteToFile` 函数用于获取并转换为 CUDA 代码。计算结果从 GPU 返回到 CPU，允许过滤和计数在 CPU 上进行。

# 列表 9-36 使用 GPU 计算 π

```

let blockIdx = new BlockDim()

let threadIdx = new ThreadIdx()

[ReflectedDefinition; GPU]:

let sample3 = (a:CUDAPointer<float32>) (b:CUDAPointer<float32>) (c:CUDAPointer<float32>)

let x = blockIdx.x

c.Set(sqrt(a[x] * a[x]) + (b[x] * b[x]), x)

let WriteToFile(2) =

let a1 = <<@sample3>>

let b = getCUDACode(a1) // 定义在列表 9-28

let commonCode = getCommonCode() // 定义在列表 9-28

System.IO.File.WriteAllText(tempFileName, commonCode + b);

let computePI() =

let len = 1000

WriteToFile2()

let execution = new GPUExecution()

let r = execution.Init(tempFileName)

let r = CURANDRandom()

let status, g = r.CreateRandomGenerator(CURANDRngType.CURUDO_DEFAULT)

if status == CURAND_SUCCESS then

    let status, 10 = r.GenerateUniform(g, len)

    let status, 11 = r.GenerateUniform(g, len)

    let output = Array.create len 0.f

    let _ = execution.Runtime.CopyToHost(UDAPointer<_>(10), output)

    let _ = execution.Runtime.CopyToHost(UDAPointer<_>(11), output)

    let r, 12 = execution.Runtime.Execute("sample3", [10; 11; 12], len)

    float (output |> Seq.float(fun n->n.f) / Seq.length) / float * 4.0

else

    fail("execution error")

```

> 注意 此程序使用了 curand 库；因此，某些类型如 `curandStatus` 定义在列表 9-9 中。生成的代码见列表 9-37。

### 列表 9-37 运行列表 9-36 的生成的代码

```cpp

#include "CUDibrary.h"

__device__ void ff_0(float* a, float* b, float* c) { int x;

x = blockIdx.x;

c[x] = sqrt((a[x]) * (a[x])) + ((b[x]) * (b[x])));

}

```

```cpp

extern "C" _global__ void sample3(float* a, float* b, float* c) {

    ff_0(a, b, c);

}

```

运行列表 9-28 代码后生成的 PTX 文件

```ptx

.version 1.4

.target sm_10, map f64_to_f32

// compiled with C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v4.2\bin..

open64/10/b.exe

// nvvpenc 4.1 built on 2012-04-07

```

```cpp

// Compiling C:/Users/taliu/AppData/Local/Temp/tmpxft_0000e3c_00000000-11_temp.cpp3.i

(C:/Users/taliu/AppData/Local/Temp/ccB1#.02796)

//-

//-

// Options:

//---

// Target:ptx, ISA:sm_10, Endian:little, Pointer Size:64

// -03 (Optimization level)

// -g0 (Debug level)

// -m2 (Report advisories)

```

```ptx

.file 1 "C:/Users/taliu/AppData/Local/Temp/tmpxft_0000e3c_00000000-10_temp.cuda2.gpu"

.file 2 "c:\program files\microsoft"

```





```

cvt.s64.s32

mul.wide.s32

%rd1, %rd1;

%rd2, %rd1;

ld.param.u64

%rd3, [_cudaram_sample3_b];\add.u64

%rd4, %rd2;

ld.param.u64

%rd5, [_cudaram_sample3_a];\add.u64

%rd6, %rd5;

ld.global.f32

%f1, [%rd4+0];

ld.global.f32

%f2, [%rd6+0];

mul.f32

%f3, %f1, %f1;

ad.f32

%f4, %f2, %f3;

sqrt.approx.f32

%f5, %f4;

ld.param.u64

%rd7, [_cudaram_sample3_c];\add.u64

%rd8, %rd7;

st.global.f32

loc 15 11

[%rd8+0], %f5;

exit;

$Wend_sample3:

} // sample3

.global.u32 error;

```

过滤可以从 CPU 移动到 GPU，如列表 9-38 所示。新版本在 `sample` 函数内部执行比较，该函数在 GPU 上执行。结果是一个由 1 和 0 组成的数组，CPU 侧可以对数组元素求和。

### 列表 9-38 执行检查和相关 CPU 函数的 GPU 函数

```

let blockIdx = new BlockDim()

let threadIdx = new ThreadIdx()

[ReflectedDefinition; GPU>]

let sample3(a:CUDAPointer<float32>, b:CUDAPointer<float32>, c:CUDAPointer<float32>) = =

  let x = blockIdx.x

if sqrt(a[x] * a[x] + b[x] * b[x]) <= 1.f then

    c.Set(1.f, x)

else

    c.Set(0.f, x)

computePI() =

let computePI = =

let len = 1000

WriteToFile(2) // 定义在列表 9-34 中

let execution = new GPUExecution()

let r = execution.Init(tempFileName)

let r = CURAND()

let status, g = r.CreateGenerator(CURANDType.CURAND_PSEUDO_DEFAULT)

if status == curandStatus.CURAND_SUCCESS then // 定义在列表 9-9

let status, 10 = r.GenerateUniform(g, len)

```

```

let status, 11 = r.GenerateUniform(0, len)

let output = Array.create len 0.f

let _ = execution.Runtime.CopyDeviceToHost(CLUDAPointer2<>(10), output)

let _ = execution.Runtime.CopyDeviceToHost(CLUDAPointer2<>(11), output)

let r, 12 = execution.Runtime.CopyDeviceToHost(output)

let r = execution.Runtime.ExecuteFunction("sample", [10; 11; 12], len, 1)

let result = execution.Runtime.CopyDeviceToHost(12, output)

float (output = |> Seq.sum) / float len * 4.0

```

现在让我们查看随机数据点数量增加时的性能。列表 9-23 显示了使用不同数组长度执行 `computePI` 的情况。从执行结果可以发现，当数组长度指数级增长时，执行时间并没有显著增加，除了第一个执行了若干次一次性初始化的操作之外。

### 列表 9-9 测量 GPU 性能

```

let computePI() =

WriteToFile2() // 定义在列表 9-34 中

let execution = execution.Init(tempFileName)

let r = execution.Stop()

```

```

let r = CURANDRandom()

let status, g = r.CreateGenerator(CURANDRngType.CURAND_PSEUDO_DEFAULT)

let sw = System.Diagnostics.Stopwatch()

```

```

if status = curandStatus.CURAND_SUCCESS then // status 定义在列表 9-9 中

let compute(len) =
