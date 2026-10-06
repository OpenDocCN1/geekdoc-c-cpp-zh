

```fsharp
let SetGeneratorOrdering(generator, order) =
    curandSetGeneratorOrdering(generator, order)

let SetQuasiRandomGeneratorDimensions(generator, dimensions) =
    curandSetQuasiRandomGeneratorDimensions(generator, dimensions)

let GenerateUniform(generator, n:int) =
    let unitSize = Marshal.SizeOf(typeof<float32>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    curandGenerateUniform(generator, devicePtr, size, (r, CUDAPointer(devicePtr)))

let GenerateUniformDouble(generator, n:int) =
    let unitSize = Marshal.SizeOf(typeof<float>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    curandGenerateUniform(generator, devicePtr, size, (r, CUDAPointer(devicePtr))

let GenerateNormal(generator, n:int, mean, stddev) =
    let unitSize = Marshal.SizeOf(typeof<float32>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    curandGenerateNormal(generator, devicePtr, size, (r, CUDAPointer(devicePtr)))

let GenerateNormalDouble(generator, n:int, stddev)dev) =let    let unitSize.Size.(typeof(float<
    let
letlet = = n

letlet devicelet = device =.default<IntPtrPtrInt    let
 = CUD =unununun.malloc(&devicePtr,device)
    let r = curandNormal =(generator,,,,,,,,,APAPinter(devicedevice))

let GenerateNormalLog(generator, n:,,,,devdev = =
letlet unit = = Marshal.Size((<float32>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    let r = curandGenerateLog(generator, devicePtr, size, (r, CUDAPointer(devicePtr)))

let GenerateNormalLogDouble(generator, n:int, mean, stddev)dev,mean,mean,mean,stddev) =
    let unitSize = Marshal.SizeOf(typeof<float>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    let r = curandGenerateLogDouble(generator, devicePtr, size, (r, CUDAPointer(devicePtr)))
```
第 9 章 使用 F# 进行 GPGPU

如果你倾向于使用类，`CUDandom` 类的定义在示例 9-11 中。

#示例 9-11 CUDandom 类定义

```fsharp
type CUDandom() =
    let is64bit = IntPtr.Size = 8

    member this.CreateGenerator(rand_type) =
        if is64bit then
            CUDandomDriver64.CreateGenerator(rand_type)
        else
            CUDandomDriver32.CreateGenerator(rand_type)
    member this.DestroyGenerator(g) =
        if is64bit then
            CUDandomDriver64.DestroyGenerator(g)
        else
            CUDandomDriver32.DestroyGenerator(g)
    member this.SetRandomSeed(g, obj) =
        if is64bit then
            CUDandomDriver64.SetRandomSeed(g, obj)
        else
            CUDandomDriver32.SetRandomSeed(g, obj)
    member this.SetGeneratorOffset(g, obj) =
        if is64bit then
            CUDandomDriver64.SetGeneratorOffset(g, obj)
        else
            CUDandomDriver32.SetGeneratorOffset(g, obj)
    member this.SetGeneratorOrdering(g, ordering) =
        if is64bit then
            CUDandomDriver64.SetGeneratorOrdering(g, ordering)
        else
            CUDandomDriver32.SetGeneratorOrdering(g, ordering)
    member this.SetQuasiRandomDimensions(g, obj) =
        if is64bit then
            CUDandomDriver64.SetQuasiRandomDimensions(g, obj)
        else
            CUDandomDriver32.SetQuasiRandomDimensions(g, obj)
    member this.GenerateUniform(g, seed) =
        if is64bit then
            CUDandomDriver64.GenerateUniform(g, seed)
        else
            CUDandomDriver32.GenerateUniform(g, seed)
    member this.GenerateUniformDouble(g, seed) =
        if is64bit then
            CUDandomDriver64.GenerateUniformDouble(g, seed)
        else
            CUDandomDriver32.GenerateUniformDouble(g, seed)
    member this.GenerateNormal(g, seed, mean, stddev) =
        if is64bit then
            CUDandomDriver64.GenerateNormal(g, seed, mean, stddev)
        else
            CUDandomDriver32.GenerateNormal(g, seed, mean, stddev)
    member this.GenerateNormalDouble(g, seed, mean, stddev) =
        if is64bit then
            CUDandomDriver64.GenerateNormalDouble(g, seed, mean, stddev)
        else
            CUDandomDriver32.GenerateNormalDouble(g, seed, mean, stddev)
    member this.GenerateNormalLog(g, seed, mean, stddev) =
        if is64bit then
            CUDandomDriver64.GenerateNormalLog(g, seed, mean, stddev)
        else
            CUDandomDriver32.GenerateNormalLog(g, seed, mean, stddev)
    member this.GenerateNormalLogDouble(g, seed, mean, stddev) =
        if is64bit then
            CUDandomDriver64.GenerateNormalLogDouble(g, seed, mean, stddev)
        else
            CUDandomDriver32.GenerateNormalLogDouble(g, seed, mean, stddev)
```

调用 `CUDandom` 所需的示例代码在列表 9-12 中所示。该示例代码生成 256 个随机数。

#列表 9-12 调用 CUDandom 类的示例代码

```fsharp
open System.Runtime.InteropServices

let test() =
    let n = 256
    let r = CUDandom()
    let status, g = r.CreateGenerator(CURANDRType.PSEUDO_DEFAULT)
    if status = CURANDStatus.SUCCESS then
        let status, v = r.GenerateUniform(g, n)
        if status = CURANDStatus.SUCCESS then
            let array : float32 = Array.Create(n)
            let nativePtr = Marshal.UnsafeOfPinnedElement(array, 0)
            let p = IntPtr(nativePtr.ToPointer())
            CUDARuntime64.cudaMemcpy(p, v, n * Marshal.SizeOf(sizeof<float32>), cudaMemcpyKind.DeviceToHost)
            Array.iter(function x -> printf("%A", x)) array
            r.DestroyGenerator(g)
        else
            printf("generation failed. status = %A", status)
            r.DestroyGenerator(g)
    else
        printf("generation failed. status = %A", status)
```

接受拒绝法（Accept rejection sampling）是一种从复杂的概率分布中生成随机样本的方法。假设我们想从目标分布 $f(x)$ 中采样，但我们知道一个容易采样的分布 $g(x)$，且对于所有 $x$，都满足 $f(x) \le Mg(x)$。算法步骤如下：从 $g(x)$ 中采样 $x$，然后从均匀分布 $[0, 1]$ 中采样 $u$。如果 $u \le f(x)/Mg$，则接受 $x$；否则，重复上述过程。

Accept rejection sampling is a method for generating random samples from a complex probability distribution. Suppose we want to sample from a target distribution $f(x)$, but we know an easier-to-sample distribution $g(x)$, such that for all $x$, $f(x) \le Mg(x)$. The algorithm steps are as follows: sample $x$ from $g(x)$, then sample $u$ from the uniform distribution $[0, 1]$. If $u \le f(x)/Mg$, then accept $x$; otherwise, repeat the process.

接受拒绝法在统计学和物理模拟中非常有用，特别是当无法直接从目标分布中进行采样时。它通过拒绝不符合目标概率的样本，来确保最终生成的样本严格遵循 $f(x)$。

