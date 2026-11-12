![](bbox=[0.11, 0.11, 0.88, 0.43])

FIGURE 7.17
Memory transfers after using shared memory.

```
if (tid < num_cipher_blocks)
    AES_decrypt_4x4_reg( &src_block[tid], &dest_blocks[tid], &expanded_key[0] );
}
```

```
__host__ __device__ void AES_decrypt_4x4_reg(
    const uint4 * const src_cipher_block,
    uint4 * const dest_cipher_block,
    KEY_T * const cipher_key)
{
    ...
}
```

The fact that we have passed a number of parameters to the device function, which in turn allows it to be called by a number of global functions and the host function, causes the compiler to insert a stack frame. We rarely if ever want the compiler to call a stack and instead want it to inline the call to the device function, thereby eliminating any need to use a stack. We can do this using the __forceinline__ directive when declaring the function as shown here:

```
__host__ __device__ __forceinline__ void AES_decrypt_4x4_reg(
    const uint4 * const src_cipher_block,
    uint4 * const dest_cipher_block,
    KEY_T * const cipher_key)
{
    ...
}
```