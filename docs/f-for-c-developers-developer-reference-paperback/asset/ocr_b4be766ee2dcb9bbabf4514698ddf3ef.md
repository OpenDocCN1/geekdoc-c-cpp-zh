```
| ErrorBinaryForCPU = 209
ErrorNotFound = 500
ErrorNotMapped = 211
ErrorNotReady = 600
ErrorUnmapFailed = 206
NotMappedAsArray = 212
NotMappedAsPointer = 213
PointerIs64Bit = 800
SizeIs64Bit = 801
ErrorUnknown = 999
```

```
module InteropLibrary=
[DllImport("cuda")]
extern CUResult cuDriverVersion(int)
```

```
type CUDADriver=
member this.Version =
let mutable version = 0
InteropLibrary.cuDriverVersion(&version), version
```

Note There is a cudaError structure defined in Listing 9-1. The cuError structure seems to serve the same purpose. However, cuError is the CUDA driver API, while cudaError is part of the CUDA runtime API. The runtime API is based on the driver API. Programming runtime APIs is simpler, but driver APIs provide better control over the device. There is no performance difference between these two types of APIs. It is recommended that you refrain from combining these kinds of APIs in one application. The function in the driver API is prefixed with cu, while the runtime API begins with cuda.

To make the GPU compute the data, the data should be first loaded into memory. The computations happen within the GPU's memory. You refer to the GPU as device and the CPU as host. The CPU memory is called the host memory, and the GPU memory is called the device memory. The memory-management function is defined in Listing 9-7. The enum type CUDAMemcpyKind defines four types of memory copy operations.

# LISTING 9-7 CUDA device memory-management function

```
namespace CUDARuntime

open System
open System.Text
open System.Collections.Generic
open System.Runtime.InteropServices
open CUDAppDataStructure
```