

```cs
[DllImport(dllName)]
extern CUBLASStatus cublasGetError()
[DllImport(dllName)]
extern CUBLASStatus cublasFree(CUDAPointer devicePtr)
[DllImport(dllName)]
extern CUBLASStatus cublasCreate_v2(CUBLASHandle& handle)
[DllImport(dllName)]
extern CUBLASStatus cublasSetStream_v2(CUBLASHandle handle, CUDAStream_t streamId)
[DllImport(dllName)]
extern CUBLASStatus cublasGetStream_v2(CUBLASHandle handle, CUDAStream_t& stream)
[DllImport(dllName)]
extern CUBLASStatus cublasGetPointerMode_v2(CUBLASHandle handle, 
	CUBLASPointerMode& mode)
[DllImport(dllName)]
extern CUBLASStatus cublasSetPointerMode_v2(CUBLASHandle handle, 
	CUBLASPointerMode mode)
[DllImport(dllName)]
extern CUBLASStatus cublasIcamax_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, int inc, result)
[DllImport(dllName)]
extern CUBLASStatus cublasIdamax_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, int inc, result)
[DllImport(dllName)]
extern CUBLASStatus cublasIsamax_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, int inc, result)
[DllImport(dllName)]
extern CUBLASStatus cublasIzamax_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, int inc, result)
[DllImport(dllName)]
extern CUBLASStatus cublasIdZamin_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, int inc, result)
[DllImport(dllName)]
extern CUBLASStatus cublasIsZamin_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, int inc, result)
[DllImport(dllName)]
extern CUBLASStatus cublasIzZamin_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, int inc, result)
[DllImport(dllName)]
extern CUBLASStatus cublasSamum_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, float alpha, float& result)
[DllImport(dllName)]
extern CUBLASStatus cublasDasum_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, double alpha, double& result)
[DllImport(dllName)]
extern CUBLASStatus cublasScasum_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, float alpha, float& result)
[DllImport(dllName)]
extern CUBLASStatus cublasDzasum_v2(CUBLASHandle handle, 
	int n, IntPtr x, int incx, double alpha, double& result)
```

552 第三部分 真实世界应用

```cs
[DllImport(dllName)]
extern CUBLASStatus cublasSaxpy_v2(CUDABLASHHandle handle,int n, float32&alpha, IntPtr x,
int incx, IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasDaxpy_v2(CUDABLASHHandle handle,int n, float&alpha, IntPtr x,
int incx, IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasSaxpy_v2(CUDABLASHHandle handle, int n,
cUDAFloatComplex&alpha, IntPtr x,
int incx, IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasZaxpy_v2(CUDABLASHHandle handle, int n,
cUDAFloatComplex&alpha, IntPtr x,
int incx, IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasScopy_v2(CUDABLASHHandle handle,int n, IntPtr x, int incx, IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasDcopy_v2(CUDABLASHHandle handle,int n, IntPtr x, int incx, IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasCcopy_v2(CUDABLASHHandle handle,int n, IntPtr x, int incx, IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasZcopy_v2(CUDABLASHHandle handle,int n, IntPtr x, int incx, IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasSdot_v2(CUDABLASHHandle handle,int n, IntPtr x, int incx, IntPtr y,int incy, float32&result)

[DllImport(dllName)]
extern CUBLASStatus cublasDdot_v2(CUDABLASHHandle handle,int n, IntPtr x, int incx,
IntPtr y, int incy, float&result)

[DllImport(dllName)]
extern CUBLASStatus cublasdot_v2(CUDABLASHHandle handle, int n, IntPtr x, int incx,
IntPtr y, int incy, CUDAFloatComplex&result)

[DllImport(dllName)]
extern CUBLASStatus cublasct_v2(CUDABLASHHandle handle, int n, IntPtr x, int incx,
IntPtr y, int incy, CUDAFloatComplex&result)

[DllImport(dllName)]
extern CUBLASStatus cublasZdot_v2(CUBLASHandle handle, int n,
cUDAFloatComplex&alpha, IntPtr x, int incx,,Ptr,, int incy, CUDAFloatComplex&result)

[DllImport(dllName)]
extern CUBLASStatus cubZZc_v2(CUBLASHandle handle, int n,
cUDAFloatComplex&alpha, IntPtr x,
int incx,Ptr y, int inc,,FloatComplex&result)

[[Import((dllName

externBLASStatusStatuslasrmrm2_v2(CUBLHandleHandle,, n,,IntPtr x,, intx,,22[result)

[DllImport(dllName)]
extern CUBLASStatus cublasDnrm2_v2(CUBLASHandle handle, int n,
IntPtr x, int incx, float&result)

[DllImport(dllName)]
extern CUBLASStatus cublasScnm2_v2(CUBLASHandle handle, int n,
IntPtr x, int incx, float32&result)

[DllImport(dllName)]
extern CUBLASStatus cublasDnrm2_v2(CUBLASHandle handle, int n,
IntPtr x, int incx, float&result)

[DllImport(dllName)]
extern CUBLASStatus cublasSrot_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr s)

[DllImport(dllName)]
extern CUBLASStatus cublasDrot_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr s)

[DllImport(dllName)]
extern CUBLASStatus cublasCrot_v2(CUDABLASHHandle handle, IntPtr a, IntPtr b,
IntPtr s)

[DllImport(dllName)]
extern CUBLASStatus cublasZrot_v2(CUDABLASHHandle handle, IntPtr a, IntPtr b,
IntPtr s)

[DllImport(dllName)]
extern CUBLASStatus cublasSrotm_v2(CUDABLASHHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr param)

[DllImport(dllName)]
extern CUBLASStatus cublasDrotm_v2(CUDABLASHHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy, IntPtr param)

[DllImport(dllName)]
extern CUBLASStatus cublasSrotmg_v2(CUDABLASHHandle handle, IntPtr d1,
IntPtr d2, IntPtr x1, IntPtr y,
param)

[DllImport(dllName)]
extern CUBLASStatus cublasDrotmg_v2(CUDABLASHHandle handle, IntPtr d1,
IntPtr d2, IntPtr x1, IntPtr y,
param)

[DllImport(dllName)]
extern CUBLASStatus cublasSscal_v2(CUDABLASHHandle handle, int n,
IntPtr alpha, IntPtr x, int incx)

[DllImport(dllName)]
extern CUBLASStatus cublasDscal_v2(CUDABLASHHandle handle, int n,
IntPtr alpha, IntPtr x, int incx)

[DllImport(dllName)]
extern CUBLASStatus cublasCscal_v2(CUDABLASHHandle handle, int n,
IntPtr alpha, IntPtr x, int incx)

[DllImport(dllName)]
extern CUBLASStatus cublasCsscal_v2(CUDABLASHHandle handle, int n,
IntPtr alpha, IntPtr x, int incx)

[DllImport(dllName)]
extern CUBLASStatus cublasZscal_v2(CUDABLASHHandle handle, int n,
IntPtr alpha, IntPtr x, int incx)

[DllImport(dllName)]
extern CUBLASStatus cublasSswap_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasDswap_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasCswap_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy)

[DllImport(dllName)]
extern CUBLASStatus cublasZswap_v2(CUBLASHandle handle, int n,
IntPtr x, int incx,
IntPtr y, int incy)
```

**注意** `dumpbin.exe` 用于检查从 CUDA BLAS 出的函数。`cublas64_<version>.DLL` 位于 `<CUDA 安装目录> C\bin` 中。来自 `dumpbin.exe` 的结果可能有两个版本。例如，`cublasZdcal` 和 `cublasZdcal_2` 函数显示在结果中。建议使用带有 `_2` 后缀的函数。

