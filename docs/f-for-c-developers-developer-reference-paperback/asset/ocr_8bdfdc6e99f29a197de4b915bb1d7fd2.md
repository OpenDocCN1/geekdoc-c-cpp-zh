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
1d.param.u64 %rd3, [cudaram_pascalTriangle_a];
add.u64 %rd4, %rd3, %rd2;
1d.param.u64 %rd5, [cudaram_pascalTriangle_b];
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

The CUDA runtime is a wrapper for managing how to load and execute functions on the GPU. *GPUExecution* is a wrapper class that also includes the function to generate the PTX. *GPUExecution* class uses nvcc.exe with a -ptx switch to generate the PTX file. In the *Init* function, *GPUExecution* calls the CUDA runtime to load the PTX file into the GPU, as shown in Listing 9-31.

**LISTING 9-31** *GPUExecution* and *CUDA array class*

```
CUDA runtime
open System
open System.Text
open System.Collections.Generic
open System.Runtime.InteropServices

type uint = uint32
```