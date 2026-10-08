In both cases, it is necessary to use CUDA streams (and likely events) to overlap CPU and GPU execution (as described in Chapter 6).

crypt.openmp contains an example of using OpenMP parallelism on the CPU and CUDA parallelism in a single application. OpenMP is a programming model for the host that users direct directives to parallel regions, similar to OpenACC. The only OpenMP-specific code added is to `omp_set_num_threads` to configure the number of CPU cores used, and the addition of an OpenMP program in the host-side computational function `h_encrypt_decrypt`. The compiler hint `#pragma omp parallel for` marks the following loop parallel and instructs OpenMP to run it across multiple CPU threads.

```
#pragma omp for
for (c = 0; c < nChunks; c++) {
    doCrypt(c, plain, key);
}
```

crypt.openmp adds logic for partitioning the workload across CPU and GPU with a new command-line argument that specifies the percentage of bytes to be encrypted or decrypted on the CPU, with the remainder of the workload offloaded to the GPU.

CPU and GPU computation is performed in parallel by queuing data transfer and kernel execution for each device in separate streams, launching the CPU threads until the asynchronous CUDA calls return to the host:

```
CALL(cudaEventRecord(startEvent));

for (d = 0; d < nDevices; d++) {
    CALL(cudaSetDevice(d));
    int start = d * chunksPerpu * CHUNK_SIZE;
    if (start + len > chunksPerpu * CHUNK_SIZE) {
        len = gpuLen - start;
    }
    encrypt_decrypt_driver(text + start, crypt + start, key, len, nThreadsPerBlock, ctxs + d);
}

int cpuStart = gpuLen;
h_encrypt_decrypt(text + cpuStart, crypt + cpuStart, key, textLen - cpuStart);

CALL(cudaEventRecord(finishEvent));
```

crypt.openmp must be compiled and linked with OpenMP support. If your NVIDIA compiler uses the gcc host compiler, you can do so by:

```
$ nvcc -Xcompiler -fopenmp -arch=sm_20 crypt.openmp -o crypt.openmp -lgomp
```

Note that crypt.openmp adds two new command-line arguments: the number of CPU cores to use (ncpus) and the percentage of the data to process on the CPU (cpu-percent). You should specify the cpu-percent command-line option using values between 0.0 and 1.0.

You can use the cpu-percent command-line argument to study how performance changes as you increase the amount of workload on the CPU.