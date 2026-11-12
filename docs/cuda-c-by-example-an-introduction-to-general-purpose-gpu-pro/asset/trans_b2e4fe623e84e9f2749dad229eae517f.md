
计算。尽管系统可能有多个 GPU（数量大于一），但为了清晰起见，我们将只使用其中两个：

```
DataStruct data[2];

data[0].deviceID = 0;
data[0].size = N/2;
data[0].a = a;
data[0].b = b;

data[1].deviceID = 1;
data[1].size = N/2;
data[1].a = a + N/2;
data[1].b = b + N/2;
```

要继续，我们将其中一个 DataStruct 变量传递给我们命名为 start_thread() 的实用函数。我们还将一个函数指针传递给 start_thread()，该指针指向由新创建的线程调用的函数；此示例的线程函数称为 routine()。函数 start_thread() 将创建一个新线程，然后调用指定的函数，并将 DataStruct 传递给该函数。routine() 的另一次调用是从默认应用程序线程进行的 [因此我们只创建了一个额外的线程]。

```
CUTThread thread = start_thread( routine, &(data[0]) );
routine( &(data[1]) );
```

在继续之前，我们让主应用程序线程通过调用 end_thread() 等待另一个线程完成。

```
end_thread( thread );
```

由于在 main() 此时两个线程都已完成，因此可以安全地清理并显示结果。

```
free( a );
free( b );

printf( "Value calculated: %f\n",
       data[0].returnValue + data[1].returnValue );

return 0;
}
```

请注意，我们对每个线程计算的结果求和。这是我们点积归约的最后一步。在另一种算法中，多个结果的组合可能涉及其他步骤。事实上，在某些应用程序中，两个 GPU 可能在完全不同的数据集上执行完全不同的代码。为了简单起见，在我们的点积示例中并非如此。

由于点积例程与您见过的其他版本相同，我们将在本节中省略它。但是，`routine()` 的内容可能值得关注。我们将 `routine()` 声明为接受并返回 `void*`，以便您可以将 `start_thread()` 代码与线程函数的任意实现一起重用。虽然我们很想为这个想法争取功劳，但在 C 中，这对回调函数来说是相当标准的做法：

```
void* routine( void *pvoidData ) {
    DataStruct *data = (DataStruct*)pvoidData;
    HANDLE_ERROR( cudaSetDevice( data->deviceID ) );
}
```

每个线程调用 `cudaSetDevice()`，并向该函数传递不同的 ID。因此，我们知道每个线程将操作不同的 GPU。这些 GPU 可能具有相同的性能，例如双 GPU GeForce GTX 295，也可能是不同的 GPU，就像系统同时拥有集成 GPU 和独立 GPU 的情况一样。这些细节对我们的应用程序并不重要，尽管它们可能对您有用。特别是，如果您依赖某个最低计算能力来启动内核，或者希望在系统的 GPU 之间对应用程序进行负载均衡，这些细节将证明很有用。如果 GPU 不同，您需要做一些工作来划分计算，以便每个 GPU 大致占用相同的时间。然而，为了本示例的目的，这些都是我们不必担心的微不足道的细节。

除了调用 cudaSetDevice() 以指定我们打算使用的 CUDA 设备之外，routine() 的此实现与第 11.11.1 节“零拷贝点积”中的普通 malloc_test() 非常相似。我们为输入的 GPU 副本分配缓冲区，并为部分结果分配一个缓冲区，然后通过 cudaMemcpy() 将每个输入数组复制到 GPU。

```
int       size = data->size;
float     *a, *b, c, *partial_c;
float     *dev_a, *dev_b, *dev_partial_c;

// allocate memory on the CPU side
a = data->a;
b = data->b;
partial_c = (float*)malloc( blocksPerGrid*sizeof(float) );

// allocate the memory on the GPU
HANDLE_ERROR( cudaMalloc( (void**)&dev_a,
                          size*sizeof(float) ) );
HANDLE_ERROR( cudaMalloc( (void**)&dev_b,
                          size*sizeof(float) ) );
HANDLE_ERROR( cudaMalloc( (void**)&dev_partial_c,
                          blocksPerGrid*sizeof(float) ) );

// copy the arrays 'a' and 'b' to the GPU
HANDLE_ERROR( cudaMemcpy( dev_a, a, size*sizeof(float),
                          cudaMemcpyHostToDevice ) );
HANDLE_ERROR( cudaMemcpy( dev_b, b, size*sizeof(float),
                          cudaMemcpyHostToDevice ) );
```

然后我们启动点积内核，将结果复制回，并在 CPU 上完成计算。

```
dot<<<blocksPerGrid, threadsPerBlock>>>( size, dev_a, dev_b,
    dev_partial_c );

// copy the array 'c' back from the GPU to the CPU
HANDLE_ERROR( cudaMemcpy( partial_c, dev_partial_c,
    blocksPerGrid*sizeof( float ),
    cudaMemcpyDeviceToHost ) );

// finish up on the CPU side
c = 0;
for (int i=0; i<blocksPerGrid; i++) {
    c += partial_c[i];
}
```

与往常一样，我们清理 GPU 缓冲区，并将计算出的点积返回到 DataStruct 的 returnValue 字段中。

```
HANDLE_ERROR( cudaFree( dev_a ) );
HANDLE_ERROR( cudaFree( dev_b ) );
HANDLE_ERROR( cudaFree( dev_partial_c ) );

// free memory on the CPU side
free( partial_c );

data->returnValue = c;
return 0;
}
```

归根结底，除了主机线程管理问题之外，使用多个 GPU 并不比使用单个 GPU 困难太多。使用我们的辅助代码来创建线程并在该线程上执行函数，这变得容易管理得多。如果您有自己的线程库，应该随时在自己的应用程序中使用它们。您只需要记住，每个 GPU 都有自己的线程，其他一切都是小菜一碟。

## 11.4 可移植锁页内存

使用多个 GPU 的最后一个重要部分涉及使用锁页内存。我们在第 10 章中了解到，锁页内存实际上是将其页面锁定在物理内存中的主机内存，以防止其被分页出去或重新分配。然而，事实证明，页面只能对单个 CPU 线程显示为锁定。也就是说，如果任何线程将其分配为锁页内存，它们将保持页面锁定状态，但只会对分配它们的线程显示为页面锁定。如果此内存的指针在线程之间共享，其他线程会将缓冲区视为标准的可分页数据。

这种行为的副作用是，当未分配锁页缓冲区的线程尝试使用它执行 cudaMemcpy() 时，复制将以标准可分页内存速度进行。如在第 10 章中所见，这种速度大约只能达到最大可实现传输速度的 50%。更糟糕的是，如果该线程尝试将 cudaMemcpyAsync() 调用入队到 CUDA 流中，该操作将失败，因为它需要锁页缓冲区才能继续。由于缓冲区对未分配它的线程来说显示为可分页，该调用将惨遭失败。即使在未来也无法工作！

但有办法解决这个问题。我们可以将锁页内存分配为可移植的，这意味着我们将被允许在主机线程之间迁移它，并允许任何线程将其视为锁页缓冲区。为此，我们使用可靠的 cudaHostAlloc() 来分配内存，但使用新标志调用它：cudaHostAllocPortable。此标志可以与您见过的其他标志一起使用，例如 cudaHostAllocWriteCombined 和 cudaHostAllocMapped。这意味着您可以将主机缓冲区分配为可移植、零拷贝和写组合的任意组合。

为了演示可移植锁页内存，我们将增强我们的多 GPU 点积应用程序。我们将改编我们最初的零拷贝点积版本，因此此版本一开始就是零拷贝和多 GPU 版本的某种混合。与本章一贯的做法一样，我们需要验证至少有两个 CUDA 兼容 GPU，并且两者都能处理零拷贝缓冲区。

```
int main( void ) {
    int deviceCount;
    HANDLE_ERROR( cudaGetDeviceCount( &deviceCount ) );
    if (deviceCount < 2) {
        printf( "We need at least two compute 1.0 or greater "
                "devices, but only found %d\n", deviceCount );
        return 0;
    }

    cudaDeviceProp prop;
    for (int i=0; i<2; i++) {
        HANDLE_ERROR( cudaGetDeviceProperties( &prop, i ) );
        if (prop.canMapHostMemory != 1) {
            printf( "Device %d cannot map memory.\n", i );
            return 0;
        }
    }
}
```

在之前的示例中，我们准备好开始在主机上分配内存以保存输入向量。然而，要分配可移植锁页内存，首先需要设置我们打算运行的 CUDA 设备。由于我们还打算使用该设备进行零拷贝内存，因此我们在 cudaSetDevice() 调用后跟随 cudaSetDeviceFlags() 调用，就像我们在第 11.1.1 节“零拷贝点积”中所做的那样。

```
float *a, *b;
HANDLE_ERROR( cudaSetDevice( 0 ) );
HANDLE_ERROR( cudaSetDeviceFlags( cudaDeviceMapHost ) );
HANDLE_ERROR( cudaHostAlloc( (void**)&a, N*sizeof(float),
                             cudaHostAllocWriteCombined |
                             cudaHostAllocMapped ) );
HANDLE_ERROR( cudaHostAlloc( (void**)&b, N*sizeof(float),
                             cudaHostAllocWriteCombined |
                             cudaHostAllocPortable |
                             cudaHostAllocMapped ) );
```
