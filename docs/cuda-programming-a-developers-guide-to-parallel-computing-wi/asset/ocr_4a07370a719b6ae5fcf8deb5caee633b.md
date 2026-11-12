With a reduced memory footprint, each `gmul` table is now 256 bytes in size, so the four tables fit easily with 1 K. As we can place a maximum of eight blocks per SM, 8 K of shared memory is now sufficient to accommodate the `gmul` tables.

Performing this shared memory optimization, however, has a problem. Indeed we move 18 GB of memory bandwidth from the L1 cache to the shared memory, and the main memory bandwidth drops by 7 MB. However, we have to move 1 K of data at the start of each block, as the shared memory is not persistent or shared between blocks. The L1 cache, however, is shared between the blocks and is currently doing a very good job of dealing with this scattered memory pattern, as the tables are entirely resident within the cache. The net improvement of speed for our 8 K of shared memory usage is almost zero, so this optimization was removed, leaving the tables in the L1 cache instead. Note this would have brought considerable improvement on compute 1.x devices, compared to global memory accesses, where there are no L1/L2 caches.

Looking back at Figure 7.16, did you notice something interesting? Did you notice we were using 1.91 GB of local storage? Local storage is the compiler spilling registers to the memory system. Prior to compute 2.0 devices this would actually go to global memory space. From compute 2.0 onward it gets contained within the L1 cache if possible, but can still cause significant unwanted global memory traffic. When compiling, the `-v` option will display a summary of the register usage from the kernel. Anytime you see the following message you have local memory being used:

```
nn bytes stack frame, nn bytes spill stores, nn bytes spill loads
```

The main issue here is the `uint4` type being used. In combination with the high register usage elsewhere this `uint4` load from global memory is immediately being spilled to local memory. A 128-bit `uint4` load was deliberately chosen to minimize the number of load transactions to global memory. By spilling it to local memory instead of holding in registers, the compiler is unnecessarily polluting the caches and causing writes back to global memory.

We can explicitly move this data item into shared memory instead of local memory by simply declaring it as an array of `__shared__` and indexing it by `threadIdx.x`. As shared memory is a per-block form of local memory, we can move the spilled register explicitly into the shared memory. Moving this parameter generates the memory view shown in Figure 7.17.

Notice how simply moving this data item to shared memory drops the local memory usage from 1.91 GB to just 256 MB, and the traffic to global memory from 183 MB to 133 MB. Our shared memory traffic is approximately double what it was before to the L1, which is largely due to the shared memory bank conflicts. These are caused by placing a 128-bit (16-byte) value into a 32-bit (4-byte) shared memory system. The compiler, however, still insists on creating a stack frame, much smaller than before, but it’s still there. The overall execution time remains stubbornly stuck at 63 ms.

To see exactly what parameters are being spilled you have to look at the PTX code, the assembly code, generated within a given kernel. Any PTX instructions such as `.st.local` or `.ld.local` are operating on local data. Local data is also declared with `local` as a prefix. It turns out the remaining local data is actually the parameter data used between the `__global__` caller and the `__device__` function, that is,

```
__global__ void AES_decode_kernel_multi_block_single_key(uint4 * const src_block,
uint4 * const dest_blocks,
KEY_T * const expanded_key,
const u32 num_cipher_blocks)
```

```
{
const u32 tid = (blockIdx.x * blockDim.x) + threadIdx.x;
```