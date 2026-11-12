
```cpp
dot<<<blocksPerGrid,threadsPerBlock>>>( dev_a, dev_b,
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

#define sum_squares(x) ( (x)*(x+1) * (2*x+1)/6 )
printf( "Does GPU value %.6g = %.6g?\n", c,
 2 * sum_squares( (float) (N - 1) ) );

// free memory on the GPU side
cudaFree( dev_a );
cudaFree( dev_b );
cudaFree( dev_partial_c );

// free memory on the CPU side
free( a );
free( b );
free( partial_c );
}
```

## 5.3.1 DOT PRODUCT OPTIMIZED (INCORRECTLY)

We quickly glossed over the second __syncthreads() in the dot product example. Now we will take a closer look at it as well as examining an attempt to improve it. If you recall, we needed the second __syncthreads() because we update our shared memory variable cache[] and need these updates to be visible to every thread on the next iteration through the loop.

```
int i = blockDim.x/2;
while (i != 0) {
    if (cacheIndex < i)
        cache[cacheIndex] += cache[cacheIndex + i];
    __syncthreads();
    i /= 2;
}
```

Observe that we update our shared memory buffer cache[] only if cacheIndex is less than i. Since cacheIndex is really just threadIdx.x, this means that only some of the threads are updating entries in the shared memory cache. Since we are using __syncthreads() only to ensure that these updates have taken place before proceeding, it stands to reason that we might see a speed improvement only if we wait for the threads that are actually writing to shared memory. We do this by moving the synchronization call inside the if () block:

```
int i = blockDim.x/2;
while (i != 0) {
    if (cacheIndex < i) {
        cache[cacheIndex] += cache[cacheIndex + i];
        __syncthreads();
    }
    i /= 2;
}
```

Although this was a valiant effort at optimization, it will not actually work. In fact, the situation is worse than that. This change to the kernel will actually cause the GPU to stop responding, forcing you to kill your program. But what could have gone so catastrophically wrong with such a seemingly innocuous change?

To answer this question, it helps to imagine every thread in the block marching through the code one line at a time. At each instruction in the program, every thread executes the same instruction, but each can operate on different data. But what happens when the instruction that every thread is supposed to execute is inside a conditional block like an if (...) ? Obviously not every thread should execute that instruction, right? For example, consider a kernel that contains the following fragment of code that intends for odd-indexed threads to update the value of some variable:

```
int myVar = 0;
if (threadIdx.x % 2 )
    myVar = threadIdx.x;
```

In the previous example, when the threads arrive at the line in bold, only the threads with odd indices will execute it since the threads with even indices do not satisfy the condition if ( threadIdx.x % 2 ). The even-numbered threads simply do nothing while the odd threads execute this instruction. When some of the threads need to execute an instruction while others don't, this situation is known as thread divergence. Under normal circumstances, divergent branches simply result in some threads remaining idle, while the other threads actually execute the instructions in the branch.

But in the case of __syncthreads(), the result is somewhat tragic. The CUDA Architecture guarantees that no thread will advance to an instruction beyond the __syncthreads() until every thread in the block has executed the __syncthreads(). Unfortunately, if the __syncthreads() sits in a divergent branch, some of the threads will never reach the __syncthreads(). Therefore, because of the guarantee that no instruction after a __syncthreads() can be executed before every thread has executed it, the hardware simply continues to wait for these threads. And waits. And waits. Forever.

This is the situation in the dot product example when we move the __syncthreads() call inside the if (...) block. Any thread with cacheIndex greater than or equal to i will never execute the __syncthreads(). This effectively hangs the processor because it results in the GPU waiting for something that will never happen.

```
if (cacheIndex < i) {
    cache[cacheIndex] += cache[cacheIndex + i];
    __syncthreads();
}
```

The moral of this story is that __syncthreads() is a powerful mechanism for ensuring that your massively parallel application still computes the correct results. But because of this potential for unintended consequences, we still need to take care when using it.

## 5.3.2 SHARED MEMORY BITMAP

We have looked at examples that use shared memory and employed __syncthreads() to ensure that data is ready before we continue. In the name of speed, you may be tempted to live dangerously and omit the __syncthreads(). We will now look at a graphical example that requires __syncthreads() for correctness. We will show you screenshots of the intended output and of the output when run without __syncthreads(). It won't be pretty.

The body of main() is identical to the GPU Julia Set example, although this time we launch multiple threads per block:

```
#include "cuda.h"
#include "../common/book.h"
#include "../common/cpu_bitmap.h"

#define DIM 1024
#define PI 3.1415926535897932f

int main( void ) {
    CPUBitmap bitmap( DIM, DIM );
    unsigned char *dev_bitmap;

    HANDLE_ERROR( cudaMalloc( (void**)&dev_bitmap,
                              bitmap.image_size() ) );

    dim3    grids(DIM/16,DIM/16);
    dim3    threads(16,16);
    kernel<<<grids,threads>>>( dev_bitmap );
    HANDLE_ERROR( cudaMemcpy( bitmap.get_ptr(), dev_bitmap,
                              bitmap.image_size(),
                              cudaMemcpyDeviceToHost ) );
    bitmap.display_and_exit();
    cudaFree( dev_bitmap );
}
```

As with the Julia Set example, each thread will be computing a pixel value for a single output location. The first thing that each thread does is compute its x and y location in the output image. This computation is identical to the tid computation in the vector addition example, although we compute it in two dimensions this time:

```
__global__ void kernel( unsigned char *ptr ) {
 // map from threadIdx/blockIdx to pixel position
 int x = threadIdx.x + blockIdx.x * blockDim.x;
 int y = threadIdx.y + blockIdx.y * blockDim.y;
 int offset = x + y * blockDim.x * gridDim.x;
}
```

Since we will be using a shared memory buffer to cache our computations, we declare one such that each thread in our 16 x 16 block has an entry.

```
__shared__ float shared[16][16];
```

Then, each thread computes a value to be stored into this buffer.

```
// now calculate the value at that position
const float period = 128.0f;
shared[threadIdx.x][threadIdx.y] =
 255 * (sinf(x*2.0f*PI/period) + 1.0f) *
 (sinf(y*2.0f*PI/period) + 1.0f) / 4.0f;
```

And lastly, we store these values back out to the pixel, reversing the order of x and y:

```
ptr[offset*4 + 0] = 0;
ptr[offset*4 + 1] = shared[15-threadIdx.x][15-threadIdx.y];
ptr[offset*4 + 2] = 0;
ptr[offset*4 + 3] = 255;
}
```

Granted, these computations are somewhat arbitrary. We've simply come up with something that will draw a grid of green spherical blobs. So after compiling and running this kernel, we output an image like the one in Figure 5.5.

What happened here? As you may have guessed from the way we set up this example, we're missing an important synchronization point. When a thread stores the computed value in shared[][] to the pixel, it is possible that the thread responsible for writing that value to shared[][] has not finished writing it yet. The only way to guarantee that this does not happen is by using __syncthreads(). Thus, the result is a corrupted picture of green blobs.

![](img/d5750f02645080d2a91292047fbe0f98_112_0.png)

Figure 5.5 A screenshot rendered without proper synchronization
