

在此版本中，我们将跳过将输入显式复制到 GPU 的步骤，而是使用零拷贝内存直接从 GPU 访问数据。此版本的点积将与我们的固定内存测试完全相同的方式设置。具体来说，我们将编写两个函数；一个将使用标准主机内存执行测试，另一个将使用零拷贝内存来保存输入和输出缓冲区，在 GPU 上完成归约。首先让我们看看点积的标准主机内存版本。我们以常规方式开始，创建计时事件，分配输入和输出缓冲区，并用数据填充我们的输入缓冲区。

```c
float malloc_test( int size ) {
    cudaEvent_t     start, stop;
    float           *a, *b, *partial_c;
    float           *dev_a, *dev_b, *dev_partial_c;
    float           elapsedTime;

    HANDLE_ERROR( cudaEventCreate( &start ) );
    HANDLE_ERROR( cudaEventCreate( &stop ) );

    // allocate memory on the CPU side
    a = (float*)malloc( size*sizeof( float ) );
    b = (float*)malloc( size*sizeof( float ) );
    partial_c = (float*)malloc( blocksPerGrid*sizeof( float ) );

    // allocate the memory on the GPU
    HANDLE_ERROR( cudaMalloc( (void**)&dev_a,
                              size*sizeof( float ) ) );
    HANDLE_ERROR( cudaMalloc( (void**)&dev_b,
                              size*sizeof( float ) ) );
    HANDLE_ERROR( cudaMalloc( (void**)&dev_partial_c,
                              blocksPerGrid*sizeof( float ) ) );

    // fill in the host memory with data
    for (int i=0; i<size; i++) {
        a[i] = i;
        b[i] = i*2;
    }
```

分配内存并创建数据后，我们可以开始计算。我们启动计时器，将输入复制到 GPU，执行点积内核，并将部分结果复制回主机。

```c
HANDLE_ERROR ( cudaEventRecord( start, 0 ) );

// copy the arrays 'a' and 'b' to the GPU
HANDLE_ERROR ( cudaMemcpy( dev_a, a, size*sizeof( float ),
                           cudaMemcpyHostToDevice ) );
HANDLE_ERROR ( cudaMemcpy( dev_b, b, size*sizeof( float ),
                           cudaMemcpyHostToDevice ) );

dot<<<blocksPerGrid,threadsPerBlock>>> ( size, dev_a, dev_b,
                                         dev_partial_c );

// copy the array 'c' back from the GPU to the CPU
HANDLE_ERROR ( cudaMemcpy( partial_c, dev_partial_c,
                           blocksPerGrid*sizeof( float ),
                           cudaMemcpyDeviceToHost ) );
```

现在我们需要像在第 5 章中所做的那样，在 CPU 上完成计算。在这样做之前，我们将停止事件计时器，因为它只测量在 GPU 上执行的工作：

```c
HANDLE_ERROR ( cudaEventRecord( stop, 0 ) );
HANDLE_ERROR ( cudaEventSynchronize( stop ) );
HANDLE_ERROR ( cudaEventElapsedTime( &elapsedTime,
                                     start, stop ) );
```

最后，我们对部分结果求和，并释放我们的输入和输出缓冲区。

```c
// finish up on the CPU side
c = 0;
for (int i=0; i<blocksPerGrid; i++) {
    c += partial_c[i];
}
```

```c
HANDLE_ERROR( cudaFree( dev_a ) );
HANDLE_ERROR( cudaFree( dev_b ) );
HANDLE_ERROR( cudaFree( dev_partial_c ) );

// free memory on the CPU side
free( a );
free( b );
free( partial_c );

// free events
HANDLE_ERROR( cudaEventDestroy( start ) );
HANDLE_ERROR( cudaEventDestroy( stop ) );

printf( "Value calculated: %f\n", c );

return elapsedTime;
}
```

使用零拷贝内存的版本将非常相似，除了内存分配之外。因此，我们首先分配输入和输出，像以前一样用数据填充输入内存：

```c
float cuda_host_alloc_test( int size ) {
    cudaEvent_t     start, stop;
    float           *a, *b, c, *partial_c;
    float           *dev_a, *dev_b, *dev_partial_c;
    float           elapsedTime;

    HANDLE_ERROR( cudaEventCreate( &start ) );
    HANDLE_ERROR( cudaEventCreate( &stop ) );

    // allocate the memory on the CPU
    HANDLE_ERROR( cudaHostAlloc( (void**)&a,
                                 size*sizeof(float),
                                 cudaHostAllocWriteCombined |
                                 cudaHostAllocMapped ) );
```

```c
HANDLE_ERROR( cudaHostAlloc( (void**)&b,
                                      size*sizeof(float),
                                      cudaHostAllocWriteCombined |
                                      cudaHostAllocMapped ) );
HANDLE_ERROR( cudaHostAlloc( (void**)&partial_c,
                                      blocksPerGrid*sizeof(float),
                                      cudaHostAllocMapped ) );

// fill in the host memory with data
for (int i=0; i<size; i++) {
    a[i] = i;
    b[i] = i*2;
}
```

与第 10 章一样，我们再次看到 cudaHostAlloc() 的运作，尽管我们现在使用 flags 参数来指定不仅仅是默认行为。标志 cudaHostAllocMapped 告诉运行时我们打算从 GPU 访问此缓冲区。换句话说，这个标志就是使我们的缓冲区成为零拷贝的原因。对于两个输入缓冲区，我们指定标志 cudaHostAllocWriteCombined。该标志表示运行时将缓冲区分配为相对于 CPU 缓存的写合并模式。该标志不会改变我们应用程序的功能，但对于仅由 GPU 读取的缓冲区来说，它代表了重要的性能增强。然而，在 CPU 也需要从缓冲区执行读取的场景中，写合并内存可能效率极低，因此在做出此决定时，您需要考虑应用程序可能的访问模式。

由于我们使用标志 cudaHostAllocMapped 分配了主机内存，因此缓冲区可以从 GPU 访问。然而，GPU 具有与 CPU 不同的虚拟内存空间，因此缓冲区在 GPU 上访问时与在 CPU 上访问时会有不同的地址。对 cudaHostAlloc() 的调用返回内存的 CPU 指针，因此我们需要调用 cudaHostGetDevicePointer() 来获取内存的有效 GPU 指针。这些指针将传递给内核，然后由 GPU 用于从我们的主机分配中读取和写入：

```c
HANDLE_ERROR( cudaHostGetDevicePointer( &dev_a, a, 0 ) );
HANDLE_ERROR( cudaHostGetDevicePointer( &dev_b, b, 0 ) );
HANDLE_ERROR( cudaHostGetDevicePointer( &dev_partial_c,
                                        partial_c, 0 ) );
```

拿到有效的设备指针后，我们准备好启动计时器并启动内核。

```c
HANDLE_ERROR( cudaEventRecord( start, 0 ) );

dot<<<blocksPerGrid,threadsPerBlock>>>( size, dev_a, dev_b,
                                        dev_partial_c );
HANDLE_ERROR( cudaThreadSynchronize() );
```

尽管指针 dev_a、dev_b 和 dev_partial_c 都位于主机上，但由于我们调用了 cudaHostGetDevicePointer()，它们在我们的内核看来就像是 GPU 内存。由于我们的部分结果已经在主机上，我们不需要费心从设备进行 cudaMemcpy()。然而，您会注意到我们通过调用 cudaThreadSynchronize() 将 CPU 与 GPU 同步。在可能更改其内容的内核执行期间，零拷贝内存的内容是未定义的。同步后，我们确定内核已完成并且我们的零拷贝缓冲区包含结果，因此我们可以停止计时器并像以前一样在 CPU 上完成计算。

```c
HANDLE_ERROR( cudaEventRecord( stop, 0 ) );
HANDLE_ERROR( cudaEventSynchronize( stop ) );
HANDLE_ERROR( cudaEventElapsedTime( &elapsedTime,
                                    start, stop ) );

// finish up on the CPU side
c = 0;
for (int i=0; i<blocksPerGrid; i++) {
    c += partial_c[i];
}
```

点积的 cudaHostAlloc() 版本中剩下的唯一事情是清理。

```c
HANDLE_ERROR( cudaFreeHost( a ) );
HANDLE_ERROR( cudaFreeHost( b ) );
HANDLE_ERROR( cudaFreeHost( partial_c ) );

// free events
HANDLE_ERROR( cudaEventDestroy( start ) );
HANDLE_ERROR( cudaEventDestroy( stop ) );

printf( "Value calculated: %f\n", c );

return elapsedTime;
}
```

您会注意到，无论我们对 cudaHostAlloc() 使用什么标志，内存始终以相同的方式释放。具体来说，调用 cudaFreeHost() 即可解决问题。

这就完成了！剩下要做的就是看看 main() 如何将所有这些连接在一起。我们需要检查的第一件事是我们的设备是否支持映射主机内存。我们以与前一章检查设备重叠相同的方式执行此操作，即调用 cudaGetDeviceProperties()。

```c
int main( void ) {
cudaDeviceProp prop;
int whichDevice;
HANDLE_ERROR( cudaGetDevice( &whichDevice ) );
HANDLE_ERROR( cudaGetDeviceProperties( &prop, whichDevice ) );
if ( prop.canMapHostMemory != 1 ) {
printf( "Device cannot map memory.\n" );
return 0;
}
}
```

