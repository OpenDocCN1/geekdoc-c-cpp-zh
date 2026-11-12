previous PTX listing. The compiler has replaced the constant values used on the kernel with literals. This is why it's always worthwhile looking into what is going on if the results are not what are expected. An extract of the GMEM PTX code for comparison is as follows:

```
ld.global.u32 %r15, [%r16, 01];
xor.b32 %r17, %r15, %r16;
```

The program is now loading a value from global memory. The constant version was not actually doing any memory reads at all. The compiler had done a substitution of the constant values for literal values when translating the C code into PTX assembly. This can be solved by declaring the constant version as an array, rather than a number of scalar variables. Thus, the new function becomes:

```
__constant__ static const u32 const_data[4] = { 0x55555555, 0x77777777, 0x33333333,
0x11111111 };
```

```
__global__ void const_test_gpu_const(u32 * const data, const u32 num_elements)
{
    const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
    if (tid < num_elements)
    {
        u32 d = const_data[0];
        for (int i = 0; i < KERNEL_LOOP; i++)
        {
            d ^= const_data[0];
            d |= const_data[1];
            d &= const_data[2];
            d |= const_data[3];
        }
        data[tid] = d;
    }
}
```

In the generated PTX code you now see

```
ld.const.u32 %r15, [%const_data+0];
mov.s32 %r16, %r10;
xor.b32 %r17, %r15, %r16;
mov.s32 %r10, %r17;
.loc 16 47 0
ld.const.u32 %r18, [%const_data+4];
mov.s32 %r19, %r10;
or.b32 %r20, %r18, %r19;
mov.s32 %r10, %r20;
```

You now have an indexed address from the start of the constant array, which is what you'd expect to see. How does this affect the results?