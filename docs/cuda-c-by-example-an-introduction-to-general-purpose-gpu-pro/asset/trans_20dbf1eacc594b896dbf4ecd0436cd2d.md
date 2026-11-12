

事实上，执行时间线可能比这更有利；一些较新的 NVIDIA GPU 支持同时执行内核和两个内存拷贝，一个拷贝到设备，一个从设备拷贝。但是，在任何支持内存拷贝与内核执行重叠的设备上，当我们使用多个流时，整体应用程序应该会加速。

尽管有这些加速应用程序的宏大计划，计算内核将保持不变。

```c
#include "../common/book.h"

#define N (1024*1024)
#define FULL_DATA_SIZE (N*20)

__global__ void kernel( int *a, int *b, int *c ) {
    int idx = threadIdx.x + blockIdx.x * blockDim.x;
    if (idx < N) {
        int idx1 = (idx + 1) % 256;
        int idx2 = (idx + 2) % 256;
        float as = (a[idx] + a[idx1] + a[idx2]) / 3.0f;
        float bs = (b[idx] + b[idx1] + b[idx2]) / 3.0f;
        c[idx] = (as + bs) / 2;
    }
}
```

与单流版本一样，我们将检查设备是否支持将计算与内存拷贝重叠。如果设备确实支持重叠，我们将像以前一样创建 CUDA 事件来为应用程序计时。

```c
int main( void ) {
    cudaDeviceProp prop;
    int whichDevice;
    HANDLE_ERROR( cudaGetDevice( &whichDevice ) );
    HANDLE_ERROR( cudaGetDeviceProperties( &prop, whichDevice ) );

    if (!prop.deviceOverlap) {
        printf( "Device will not handle overlaps, so no "
                "speed up from streams\n" );
        return 0;
    }

    cudaEvent_t     start, stop;
    float           elapsedTime;

    // start the timers
    HANDLE_ERROR( cudaEventCreate( &start ) );
    HANDLE_ERROR( cudaEventCreate( &stop ) );
    HANDLE_ERROR( cudaEventRecord( start, 0 ) );
```

接下来，我们将像在上一节代码版本中创建单流一样创建两个流。

```c
// initialize the streams
cudaStream_t  stream0, stream1;
HANDLE_ERROR( cudaStreamCreate( &stream0 ) );
HANDLE_ERROR( cudaStreamCreate( &stream1 ) );
```

我们假设主机上仍然有两个输入缓冲区和一个输出缓冲区。输入缓冲区的填充方式与此应用程序单流版本完全相同，即填充随机数据。但是，既然我们打算使用两个流来处理数据，我们就分配两组相同的 GPU 缓冲区，以便每个流可以独立地处理输入的数据块。

```c
int *host_a, *host_b, *host_c;
int *dev_a0, *dev_b0, *dev_c0; // GPU buffers for stream0
int *dev_a1, *dev_b1, *dev_c1; // GPU buffers for stream1

// allocate the memory on the GPU
HANDLE_ERROR( cudaMalloc( (void**)&dev_a0,
                          N * sizeof(int) ) );
HANDLE_ERROR( cudaMalloc( (void**)&dev_b0,
    N * sizeof(int) ) );
HANDLE_ERROR( cudaMalloc( (void**)&dev_c0,
    N * sizeof(int) ) );
HANDLE_ERROR( cudaMalloc( (void**)&dev_a1,
    N * sizeof(int) ) );
HANDLE_ERROR( cudaMalloc( (void**)&dev_b1,
    N * sizeof(int) ) );
HANDLE_ERROR( cudaMalloc( (void**)&dev_c1,
    N * sizeof(int) ) );

// allocate page-locked memory, used to stream
HANDLE_ERROR( cudaHostAlloc( (void**)&host_a,
    FULL_DATA_SIZE * sizeof(int),
    cudaHostAllocDefault ) );
HANDLE_ERROR( cudaHostAlloc( (void**)&host_b,
    FULL_DATA_SIZE * sizeof(int),
    cudaHostAllocDefault ) );
HANDLE_ERROR( cudaHostAlloc( (void**)&host_c,
    FULL_DATA_SIZE * sizeof(int),
    cudaHostAllocDefault ) );

for (int i=0; i<FULL_DATA_SIZE; i++) {
    host_a[i] = rand();
    host_b[i] = rand();
}
```

然后，我们像在首次尝试此应用程序时一样遍历输入的数据块。但是，既然我们现在使用两个流，在 `for ()` 循环的每次迭代中处理的数据量是原来的两倍。在 stream0 中，我们将 a 和 b 的异步拷贝排队到 GPU，排队一个内核执行，然后将数据拷贝回 c 排队：

```cpp
// now loop over full data, in bite-sized chunks
for (int i = 0; i < FULL_DATA_SIZE; i += N*2) {
    // copy the locked memory to the device, async
    HANDLE_ERROR( cudaMemcpyAsync( dev_a0, host_a+i,
        N * sizeof(int),
        cudaMemcpyHostToDevice,
        stream0 ) );
    HANDLE_ERROR( cudaMemcpyAsync( dev_b0, host_b+i,
        N * sizeof(int),
        cudaMemcpyHostToDevice,
        stream0 ) );
    kernel<<<N/256,256,0,stream0>>>( dev_a0, dev_b0, dev_c0 );
    // copy the data from device to locked memory
    HANDLE_ERROR( cudaMemcpyAsync( host_c+i, dev_c0,
        N * sizeof(int),
        cudaMemcpyDeviceToHost,
        stream0 ) );

    // copy the locked memory to the device, async
    HANDLE_ERROR( cudaMemcpyAsync( dev_a1, host_a+i+N,
        N * sizeof(int),
        cudaMemcpyHostToDevice,
        stream1 ) );
    HANDLE_ERROR( cudaMemcpyAsync( dev_b1, host_b+i+N,
        N * sizeof(int),
        cudaMemcpyHostToDevice,
        stream1 ) );

    kernel<<<N/256, 256, 0, stream1>>>( dev_a1, dev_b1, dev_c1 );

    // copy the data from device to locked memory
    HANDLE_ERROR( cudaMemcpyAsync( host_c+i+N, dev_c1,
                             N * sizeof(int),
                             cudaMemcpyDeviceToHost,
                             stream1 ) );
}
```

因此，我们的 `for()` 循环继续进行，交替地将每个数据块排队到不同的流中，直到所有输入数据都已排队等待处理。终止 `for()` 循环后，在停止应用程序计时器之前，我们将 GPU 与 CPU 同步。由于我们使用两个流，需要对两个流都进行同步。

```c
HANDLE_ERROR( cudaStreamSynchronize( stream0 ) );
HANDLE_ERROR( cudaStreamSynchronize( stream1 ) );
```

我们以与单流实现相同的方式结束 `main()`。我们停止计时器，显示经过的时间，并进行清理。当然，我们记得现在需要销毁两个流并释放两倍数量的 GPU 缓冲区，但除此之外，这段代码与我们之前看到的完全相同：

```c
HANDLE_ERROR( cudaEventRecord( stop, 0 ) );

HANDLE_ERROR( cudaEventSynchronize( stop ) );
HANDLE_ERROR( cudaEventElapsedTime( &elapsedTime,
                                      start, stop ) );
printf( "Time taken:  %3.1f ms\n", elapsedTime );

// cleanup the streams and memory
HANDLE_ERROR( cudaFreeHost( host_a ) );
HANDLE_ERROR( cudaFreeHost( host_b ) );
HANDLE_ERROR( cudaFreeHost( host_c ) );
HANDLE_ERROR( cudaFree( dev_a0 ) );
HANDLE_ERROR( cudaFree( dev_b0 ) );
HANDLE_ERROR( cudaFree( dev_c0 ) );
HANDLE_ERROR( cudaFree( dev_a1 ) );
HANDLE_ERROR( cudaFree( dev_b1 ) );
HANDLE_ERROR( cudaFree( dev_c1 ) );
HANDLE_ERROR( cudaStreamDestroy( stream0 ) );
HANDLE_ERROR( cudaStreamDestroy( stream1 ) );

return 0;
}
```

我们在 GeForce GTX 285 上对第 10.3 节“使用单个 CUDA 流”中的原始单流实现和改进后的双流版本进行了基准测试。原始版本运行完成需要 62ms。修改为使用两个流后，需要 61ms。

糟糕。

好吧，好消息是这就是我们费心为应用程序计时的原因。有时，我们最出于好意的性能“增强”只不过是给代码引入不必要的复杂性。

但为什么这个应用程序没有变快呢？我们甚至说过它会变快！不过，还不要失去希望，因为我们实际上可以用第二个流来加速单流版本，但我们需要更多地了解 CUDA 驱动程序如何处理流，才能获得设备重叠的好处。要了解流在幕后的工作原理，我们需要同时查看 CUDA 驱动程序和 CUDA 硬件架构的工作方式。

## 10.6 GPU 工作调度

虽然流在逻辑上是要在 GPU 上执行的独立操作队列，但事实证明，这种抽象并不完全匹配 GPU 的排队机制。作为程序员，我们将流视为由内存拷贝和内核混合而成的有序操作序列。

