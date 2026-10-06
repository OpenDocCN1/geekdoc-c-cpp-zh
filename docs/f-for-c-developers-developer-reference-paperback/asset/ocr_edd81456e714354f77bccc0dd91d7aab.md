```
<Struct>
type sizeT =
val value : IntPtr
new (n:int) = { value = IntPtr(n) }
new (n:int64) = { value = IntPtr(n) }
```

```
<Struct>
type CUDADeviceProp = =
[MarshaAs(UnmanagedType.ByArray,SizeCount = 256)]
val nameChar : char array
val totalGlobalMem : sizeT
val sharedMemPerBlock : sizeT
val regsPerBlock : int
val warpSize : int
val memPitch : sizeT
val maxThreadsBlock : int
[MarshaAs(UnmanagedType.ByArray,SizeCount = 3)]
val maxThreadsDim : int array
[MarshaAs(UnmanagedType.ByArray,SizeCount = 3)]
val maxGridSize : int array
val clockRate : int
val totalConstMem : sizeT
val major : int
val minor : int
val textureAlignment : sizeT
val deviceOverlap : int
val multiProcessorCount : int
val kernelIsEnabled : int
val integrated : int
val canHostMemory : int
val computeMode : int
val maxTextureID : int
[MarshaAs(UnmanagedType.ByArray,SizeCount = 2)]
val maxTexture2 : int array
[MarshaAs(UnmanagedType.ByArray,SizeCount = 3)]
val maxTexture3D : int array
[MarshaAs(UnmanagedType.ByArray,SizeCount = 2)]
val maxTexture3DLayered : int array
[MarshaAs(UnmanagedType.ByArray,SizeCount = 3)]
val maxTexture2Layered : int array
val surfaceAlignment : sizeT
val concurrentKernel : int
val ECCEnabled : int
val pciBusID : int
val pciDeviceID : int
val pciDomainID : int
val tDriver : int
val asyncEngineCount : int
val unifiedAddressing : int
val memoryClockRate : int
val memoryBusWidth : int
val l2CacheSize : int
val maxThreadsPerProcessor : int
member this.Name = String(this.nameChar,'\000')
```

CHAPTER 9 GPGPU with F# 533