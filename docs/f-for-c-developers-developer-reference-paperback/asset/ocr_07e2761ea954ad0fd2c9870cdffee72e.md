```
let SetGeneratorOrdering(generator, order) =
    curandSetGeneratorOrdering(generator, order)

let SetQuasiRandomGeneratorDimensions(generator, dimensions) =
    curandSetQuasiRandomGeneratorDimensions(generator, dimensions)

let GenerateUniform(generator, n:int) =
    let unitSize = Marshal.SizeOf(typeof<float32>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    curandGenerateUniform(generator, devicePtr, size, (r, CUDAPointer(devicePtr))

 GenerateUniformDouble(generator, n:int) =
    let unitSize = Marshal.SizeOf(typeof<float>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    curandGenerateUniform(generator, devicePtr, size, (r, CUDAPointer(devicePtr))

 GenerateNormal(generator, n:int, mean, stddev) =
    let unitSize = Marshal.SizeOf(typeof<float32>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    let r = curandGenerateNormal(generator, devicePtr, size, mean, stddev), (r, CUDAPointer(devicePtr))

 GenerateNormalDouble(generator, n:int, mean, stddev) =
    let unitSize = Marshal.SizeOf(typeof<float32>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    let r = curandGenerateNormalDouble(generator, devicePtr, size, mean, stddev), (r, CUDAPointer(devicePtr))

 GenerateNormalLog(generator, n:int, mean, stddev) =
    let unitSize = Marshal.SizeOf(typeof<float32>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    let r = curandGenerateNormalLog(generator, devicePtr, size, mean, stddev), (r, CUDAPointer(devicePtr))

 GenerateNormalLogDouble(generator, n:int, mean, stddev) =
    let unitSize = Marshal.SizeOf(typeof<float>)
    let size = n * unitSize
    let mutable devicePtr = Unchecked.default<IntPtr>()
    let r = CUDARuntime64.malloc(&devicePtr, size)
    let r = curandGenerateLogDouble(generator, devicePtr, size, mean, stddev), (r, CUDAPointer(devicePtr))
```

CHAPTER 9 GPGPU with F# 547