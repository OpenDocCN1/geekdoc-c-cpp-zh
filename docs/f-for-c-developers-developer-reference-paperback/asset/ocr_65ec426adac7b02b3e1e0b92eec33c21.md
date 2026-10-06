```
let copyToDevice(array) =
let nativePtr = Marshal.UnsafeAddrOfPinnedArrayElement(array, 0)
let p = System.IntPtr(nativePtr.ToPointer())
let mutable dst = IntPtr()
let count = SizeT(Marshal.SizeOf<float32>() * array.Length)
let r = CUDRuntime.runtime64.cudaMalloc(&dst, count)

if r = cudaError.cudaSuccess then
    let r = CUDRuntime.runtime64.cudaMemcpy(
        dst,
        p,
        count,
        CudaMemcpyKind.cudaMemcpyHostToDevice
    )
    if r = cudaError.cudaSuccess then
        Some dst
    else
        None

let mutable handle = CADHandle()
let r = CUBLASDriver64.cublasInit()
let r = CUBLASDriver64.cublasCreatev2(&handle)
let deviceA = copyToDevice(a)
let deviceB = copyToDevice(b)
let mutable result = 1.f

match deviceA, deviceB with
| Some(pA), Some(pB) ->
    let status = CUBLASDriver64.cublasSdot_v2(
        handle,
        Marshal.SizeOf(sizeof<float32>()) * n,
        pA,
        1,
        pB,
        1,
        &result
    )
    printf("result is %A", result)
| _ -> failwith("computation error")
```

# # F# Quotation and Transform

The F# quotation is a tree structure that presents the current F# program structure. The ReflectedDefinition attribute is the key attribute used to get an F# quotation. According to MSDN (http://msdn.microsoft.com/en-us/library/ee353643.aspx), here is how you use it:

Add this attribute to the let-binding of a top-level value to make the expression that implements the value available for runtime.