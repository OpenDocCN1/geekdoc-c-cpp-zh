```
[<DllImport(dllName)>\nextern CUBLASStatus cublasZdotu_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, CUDAFloatComplex&esult)
[<DllImport(dllName)>\nextern CUBLASStatus cublasZdotc_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, CUDAFloatComplex&result)
[<DllImport(dllName)>\nextern CUBLASStatus cublasSrm2_v2(CUBLASHandle handle, int n,
IntPtr x, int incx, float32&result)
[<DllImport(dllName)>\nextern CUBLASStatus cublasDnrm2_v2(CUBLASHandle handle, int n,
IntPtr x, int incx, float&result)
[<DllImport(dllName)>\nextern CUBLASStatus cublasScnm2_v2(CUBLASHandle handle, int n,
IntPtr x, int incx, float32&result)
[<DllImport(dllName)>\nextern CUBLASStatus cublasDnrm2_v2(CUBLASHandle handle, int n,
IntPtr x, int incx, float&result)
[<DllImport(dllName)>\nextern CUBLASStatus cublasSrot_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr c, IntPtr s)
[<DllImport(dllName)>\nextern CUBLASStatus cublasDrot_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr c, IntPtr s)
[<DllImport(dllName)>\nextern CUBLASStatus cublasCrot_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr c, IntPtr s)
[<DllImport(dllName)>\nextern CUBLASStatus cublasCsrot_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr c, IntPtr s)
[<DllImport(dllName)>\nextern CUBLASStatus cublasZrot_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr c, IntPtr s)
[<DllImport(dllName)>\nextern CUBLASStatus cublasZzrot_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr c, IntPtr s)
[<DllImport(dllName)>\nextern CUBLASStatus cublasSrotg_v2(CUBLASHandle handle, int n,
IntPtr a, IntPtr b, IntPtr c,
IntPtr s)
[<DllImport(dllName)>\nextern CUBLASStatus cublasDrotg_v2(CUBLASHandle handle, int n,
IntPtr a, IntPtr b, IntPtr c,
IntPtr s)
```