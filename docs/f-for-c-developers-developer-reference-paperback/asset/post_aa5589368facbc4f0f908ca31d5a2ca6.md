
```
$LDwbegin_sample2:
.loc 16 10 0
cvt.s32.u16 %r1, %ctaid.x;
cavat.s64.s32 %rd1, %r1;
mul.wide.size %rd2, %r1, 8;
ld.param.u64 %rd3, [%cudarp_sample2_c];
add.u64 %rd4, %rd3, %rd2;
ld.param.u64 %rd5, [%cudarp_sample2_b];
ld.param.u64 %rd6, [%cudarp_sample2_a];
add.u64 %rd7, %rd2, %rd5;
ld.global.f64 %fd1, [%rd7+0];
add.u64 %fd8, %rd6;
ld.global.f64 %fd2, [%rd8+0];
add.f64 %fd3, %fd1, %fd2;
st.global.f64 %fd3, [%rd4+0];
.loc 16 14 0
mov.u32 %r2, 0;
setp.le.s32 $p1, %r1, %r2;
@%p1 br $lt1_3074;
mov.s32 %r3, %r1;
.loc 16 10 0
ld.param.u64 %rd6, [%cudarp_sample2_a];
.loc 16 14 0
mov.s64 %rd9, %rd6;
.loc 16 10 0
ld.param.u64 %rd5, [%cudarp_sample2_b];
.loc 16 14 0
mov.s64 %rd10, %rd5;
mov.s32 %r4, 0;
mov.s32 %r5, %r3
$lt1_3586:
// clooop Loop body line 14, nesting depth: 1, estimated iterations: unknown
.loc 16 17 0
ld.global.f64 %fd4, [%rd9+0];
ld.global.f64 %fd5, [%rd10+0];
add.f64 %fd6, %fd4, %fd5;
st.global.f64 %fd6, [%rd4+0];
add.s32 %r4, %r4, 1;
add.u64 %rd10, %rd8, 0;
add.u64 %rd9, %rd9, 8;
setp.ne32 %p2, %r4, %r1;
@%p2 br $lt1_3574;
.loc 16 38 0
$LDwend_sample2:
} // sample2
```

```
.entry_pascalTriangle (
  .param.u64 __cudarp_pascalTriangle_a,
  .param.u64 __cudarp_pascalTriangle_b)
{
  .reg.u32 %k<4>;
```

.reg .u64 %rd=8;
.reg .f32 %f<3>;
.reg .pred %p<3>;
loc 16 39 0
$LWbegin_pascalTriangle:
loc 16 40 0
cvt.s32.u16 %rd1, %ctaid.x;
cvt.s64.s32 %rd1, %rd2;
mul.wide.s32 %rd2, %rd4;
1d.param.u64 %rd3, [cudarp_pascalTriangle_a];
add.u64 %rd4, %rd3, %rd2;
1d.param.u64 %rd5, [cudarp_pascalTriangle_b];
add.u64 %rd6, %rd5, %rd2;
1d.global.f32 %f1, [%rd4+0];
mov.u32 %r2, 0;
setp.ne.s32 %p1, %r2;
@p1 bra $lt_2_1282;
loc 16 28 0
st.global.f32 [%rd6+0], %f1;
bra.uni $lt_2_1026;
loc 16 29 0
ld.global.f32 %f2, [%rd4+4];
add.f32 %f3, %f2, %f1;
st.global.f32 [%rd6+0], %f3;
$lt_2_1026:
loc 16 41 0
exit;
$Lwend_pascalTriangle:
// pascaltriangle
.global .u32 error;
```

The CUDA runtime is a wrapper for managing how to load and execute functions on the GPU. *GPUExecution* is a wrapper class that includes the function to generate PTX. *GPUExecution* class uses nvcc with a -ptx switch to generate PTX file. In the *Init* function, *GPUExecution* calls the CUDA runtime to load PTX file into the GPU, as shown in Listing 9-31.

**LISTING 9-31 *GPUExecution* and *CUDA array class***

```csharp
CUDA runtime;
open System.Text;
open System.Collections.Generic;
open System.InteropServices;

type uint = uint32;

<Struct>
type CUDodule = val Pointer : IntPtr;

<Struct>
type CUDevice = val Pointer : int;

<Struct>
type CUDAContext = val Pointer : IntPtr;

<Struct>
type CUDAFunction = val Pointer : IntPtr;

module CudaStructureExtensions
let is64Bit = IntPtr.Size

module InteropLibrary =
[DllImport("nvcuda")]
extern CUResult cuModuleLoad(CUDodule& m, string fn)

[DllImport("nvcuda")]
extern CUResult cuDriverVersion(int& driverVersion)

[DllImport("nvcuda")]
extern CUResult cuCreate(uint flags)
externEntryPoint = "cuctx_create_v2"
extern CUResult cuCreateContext(CUDAContext& pctx, uint flags, CUDevice dev)
extern CUResult cuDeviceSet(CUDevice device, int ordinal)
extern CUResult cuModuleGetFunction(CUDAFunction& hfunc, CUDodule mod, string name)
extern CUResult cuFunctionSetBlockSize(CUDAFunction hfunc, int x, y, z)
extern CUResult cuLaunch(CUDAFunction f)
extern CUResult cuLaunchGrid(CUDAFunction f, int grid_width, int grid_height)
extern IntPtr = "cuMemAlloc_v2"
extern CUResult cuAlloc(IntPtr dptr, uint bytes)
extern IntPtr = "cuMemDtoH_v2"
extern CUResult cuMemDtoToHost(IntPtr dstHost, srcDevice, uintCount)
extern IntPtr = "cuMemHToD"
extern CUResult cuMemHostToD(IntPtr dstDevice, IntPtr srcHost, uintCount)
extern IntPtr = "cuMemFree_v2"
extern CUResult cuFree(IntPtr dptr)

[DllImport("nvcuda")]
extern CUResult cuParamSet(CUDAFunction hfunc, int offset, int value)

[DllImport("nvcuda")]
extern CUResult cuParamSet(CUDAFunction hfunc, int offset, float value)

[DllImport("nvcuda")]
extern CUResult cuParamSet(CUDAFunction hfunc, int offset, int64 value, uint numbytes)

[DllImport("nvcuda")]
extern CUResult cuParamSetSize(CUDAFunction hfunc, uint numbytes)

[DllImport("nvcuda")]
extern CUResult cuMemsetD8(CUDevice deviceType, byte c, uint n)

[DllImport("nvcuda")]
extern CUResult cuMemsetD16(CUDevice deviceType, uint16 c, uint n)
```

```csharp
type CUDAArray<T>(Pointer, size; runtime:CUDARuntime)
let unitSize = uint32(sizeof<T>)
interface IDisposable{
    this.Dispose() = runtime.Free(Pointer) | ignore
    this.Runtime.with(get()) = runtime
    this.SizeInBy.with(get()) = size
    this.Pointer.with(get()) = CUDAPointer
    this.UnitSize.with(get()) = unitSize
    this.Size.with(get()) = int(size.SizeInBytes / this.UnitSize)
    this.ToArray<T>() =
    let out = Array.create(int(size)).Unchecked.defaultof<T>
    this.Runtime.CopyDeviceToHost(this.Pointer, out)
}

and CUDARuntime(deviceID) =
let mutable device = CUDevice()
let mutable deviceContext = CudaContext()
let mutable m = CUDAModule()

let init() = {
let r = InteropLibrary.cuInit(deviceID)
let r = InteropLibrary.cuDeviceGet(&device, int(deviceID))
let r = InteropLibrary.cuCtxCreate(&deviceContext, deviceContext, device)
()}
do init() =

let align(offset, alignment) = offset + alignment - 1 &&& (alignment - 1);
new() = new CUDARuntime(Ou)

interface IDisposable{
    this.Dispose() = ()
}

member this.LoadModule(fn) =
(InteropLibrary.cuModuleLoad(&fn, m)
member this.Version
    with get() =
    let mutable a = 0
    (InteropLibrary.cuDriverVersion(&a), a)
member this.Is64Bit with get() = CudaDataStructureExtensions.is64Bit
```

```csharp
member this.GetFunction(fn)
let mutable f = CUDAFunction()
(InteropLibrary.cuModuleGetFunction(&fn, m, fn), f)
member this.ExecuteFunction(fn, x, y) =
let r, f = this.GetFunction(fn)
if r = CUResult.Success then
InteropLibrary.cuLaunchGrid(f, x, y)
else
member this.ExecuteFunction(fn) =
let r, f = this.GetFunction(fn)
if r = CUResult.Success then
InteropLibrary.cuLaunch(f)
```
