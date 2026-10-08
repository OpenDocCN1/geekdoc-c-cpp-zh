# Using the Runtime API to Query GPU Information

Many functions are available in the CUDA runtime API to help you manage devices. You can use the following function to query all information about GPU devices:

```
cudaError_t cudaGetDeviceProperties(cudaDeviceProp* prop, int device);
```

The properties of the GPU device are returned in the cudaDeviceProp structure, which you can find online at: http://docs.nvidia.com/cuda/cuda-runtime-api/index#structcudaDeviceProp.

Listing 2-8 provides an example that queries generally useful properties of interest. Compile and run it with the following:

```
$ nvcc checkDeviceInfo.cu -o checkDeviceInfo
./checkDeviceInfo
```

Depending on your configuration, checkDeviceInfo will report different information on the installed devices. A sample output is:

```
/checkDeviceInfo Starting...
Detected 2 CUDA device(s)
Device 0: "Tesla M200"
CUDA Driver Version / Runtime Version: 5.5 / 5.5
CUDA Capability Major/Minor version number: 2.0
Total amount of global memory: 5.25 Megabytes (563654752 bytes)
GPU clock: 1147 MHz (1.15 GHz)
Memory clock: 1556 MHz
Memory Bus Width: 384-bit
L2 Cache: 76412 bytes
Max Texture Dimension Size (x,y,z): 2D=(65536,65535), 3D=(2048,2048,2048)
Max Layer Texture Size (dim x layers): 16D=(16384, 16384, 2048)
Total amount of constant memory: 65536 bytes
Total amount of shared memory per block: 49152 bytes
Total number of registers available per block: 32768
Warp size: 32
Maximum number of threads per multiprocessor: 1536
Maximum number of threads per block: 1024
Maximum sizes of each dimension of a block: 1024 x 1024 x 64
Maximum sizes of each dimension of a grid: 65535 x 65535 x 65535
Maximum memory pitch: 2147483647 bytes
```

> LISTING 2-8: Query device information with the runtime API (checkDeviceInfo.cu)

```
#include <cuda_runtime.h>
#include <stdio.h>

int main(int argc, char **argv) {
    printf("%s Starting...\n", argv[0]);

    int deviceCount = 0;
    cudaError_t error_id = cudaGetDeviceCount(&deviceCount);

    continues
```