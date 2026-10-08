The remaining lines show the stack trace from the location where the kernel was launched that caused this hazard:

```
=======
Saved host backtrack up to driver entry point at kernel launch time
=======
Host Frame:/opt/cuda/driver/lib64/libcuda.so (cuLaunchKernel +
=======
0xc3dc) [0xc9dec6]
=======
Host Frame:/opt/cuda/5.0.35/lib64/libcuda.so.5 [0x11d4]
=======
Host Frame:/opt/cuda/5.0.35/lib64/libcudart.so.5.0 (cudaLaunch +
0x182) [0x38152]
=======
Host Frame:/debug-hazards (__ZcudaLaunchIcE9cudaError_PT + 0x189)
[0x1490]
=======
Host Frame:/debug-hazards
[__240_device_stub (__Z16simple_reductionPi_iPs_ii_i + Oxab) [0x135a]
=======
Host Frame:/debug-hazards (__Z16simple_reductionPi_i + Ox30)
[0x1398]
=======
Host Frame:/debug-hazards (main + 0x2c2) [0x1142]
Host Frame:/lib64/libc.so.6 (_libc_start_main + 0xfd) [0xlecdd]
=======
Host Frame:/debug-hazards [0xd99]
```

Now the information provided for the writing reading thread can be used to analyze the hazard. Recall that the writing thread was at line 50 in the debug-hazards.cu, executing the function simple_reduction. The reading thread was 66 in the same file and function. The relevant lines are highlighted here for:

```
if (tid < N)
{
    local_mem[local_id] = input_values[tid];
}

// Required for correctness
__syncthreads();

/*
* Perform the local reduction across values written to shared memory
* by threads in this block.
*/
if (local_id == 0)
{
    int sum = 0;
    for (i = 0; i < local_dim; i++)
        sum = sum + local_mem[i];
}
```

The conflict is between a write to local_mem[local_id] and a read from local_mem[i]. The reading thread is scanning through every shared memory at the same time as the writing thread is filling one of them. In the case of this application, the desired behavior is to ensure that all writes complete before the reading thread starts scanning memory, and that no additional writes are performed before the scan. Because the error reported was identified as a read-after-write, it must mean that synchronization is missing between the reads being performed as part of the scan and the writes to local memory. You have a condition where reads are being performed on memory locations before they have been written. As a first attempt at eliminating this race condition, try uncommenting the __syncthreads on line 54, rebuild and rerun with the