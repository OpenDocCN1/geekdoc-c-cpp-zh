
```
}
}
if ( success ) printf( "We did it!\n" );

// free the memory allocated on the GPU
cudaFree( dev_a );
cudaFree( dev_b );
cudaFree( dev_c );

return 0;
}
```

### 5.2.2 GPU RIPPLE USING THREADS

As with the previous chapter, we will reward your patience with vector addition by presenting a more fun example that demonstrates some of the techniques we've been using. We will again use our GPU computing power to generate pictures procedurally. But to make things even more interesting, this time we will animate them. But don't worry, we've packaged all the unrelated animation code into helper functions so you won't have to master any graphics or animation.

```
struct DataBlock {
    unsigned char *dev_bitmap;
    CPUAnimBitmap *bitmap;
};

// clean up memory allocated on the GPU
void cleanup( DataBlock *d ) {
    cudaFree( d->dev_bitmap );
}

int main( void ) {
    DataBlock data;
    CPUAnimBitmap bitmap( DIM, DIM, &data );
    data.bitmap = &bitmap;
HANDLE_ERROR( cudaMalloc( (void**)&data.dev_bitmap,
 bitmap.image_size() ) );
 bitmap.anim_and_exit( (void (*)(void*,int))generate_frame,
 (void (*)(void*))cleanup );
}
```

Most of the complexity of main() is hidden in the helper class CPUAnimBitmap. You will notice that we again have a pattern of doing a cudaMalloc(), executing device code that uses the allocated memory, and then cleaning up with cudaFree(). This should be old hat to you by now.

In this example, we have slightly convoluted the means by which we accomplish the middle step, "executing device code that uses the allocated memory." We pass the anim_and_exit() method a function pointer to generate_frame(). This function will be called by the class every time it wants to generate a new frame of the animation.

```
void generate_frame( DataBlock *d, int ticks ) {
 dim3 blocks(DIM/16,DIM/16);
 dim3 threads(16,16);
 kernel<<<blocks,threads>>>( d->dev_bitmap, ticks );
 HANDLE_ERROR( cudaMemcpy( d->bitmap->get_ptr(),
 d->dev_bitmap,
 d->bitmap->image_size(),
 cudaMemcpyDeviceToHost ) );
}
```

Although this function consists only of four lines, they all involve important CUDA C concepts. First, we declare two two-dimensional variables, blocks and threads. As our naming convention makes painfully obvious, the variable blocks represents the number of parallel blocks we will launch in our grid. The variable threads represents the number of threads we will launch per block. Because we are generating an image, we use two-dimensional indexing so that each thread will have a unique (x,y) index that we can easily put into correspondence with a pixel in the output image. We have chosen to use blocks that consist of a 16 x 16 array of threads. If the image has DIM x DIM pixels, we need to launch DIM/16 x DIM/16 blocks to get one thread per pixel. Figure 5.2 shows how this block and thread configuration would look in a (ridiculously) small, 48-pixel-wide, 32-pixel-high image.

![](img/d5750f02645080d2a91292047fbe0f98_91_0.png)

Figure 5.2 A 2D hierarchy of blocks and threads that could be used to process a 48 x 32 pixel image using one thread per pixel

If you have done any multithreaded CPU programming, you may be wondering why we would launch so many threads. For example, to render a full high-definition animation at 1920 x 1080, this method would create more than 2 million threads. Although we routinely create and schedule this many threads on a GPU, one would not dream of creating this many threads on a CPU. Because CPU thread management and scheduling must be done in software, it simply cannot scale to the number of threads that a GPU can. Because we can simply create a thread for each data element we want to process, parallel programming on a GPU can be far simpler than on a CPU.

After declaring the variables that hold the dimensions of our launch, we simply launch the kernel that will compute our pixel values.

```
kernel<<< blocks,threads>>>( d->dev_bitmap, ticks );
```

The kernel will need two pieces of information that we pass as parameters. First, it needs a pointer to device memory that holds the output pixels. This is a global variable that had its memory allocated in `main()`. But the variable is "global" only for host code, so we need to pass it as a parameter to ensure that the CUDA runtime will make it available for our device code.

Second, our kernel will need to know the current animation time so it can generate the correct frame. The current time, `ticks`, is passed to the `generate_frame()` function from the infrastructure code in `CPUAnimBitmap`, so we can simply pass this on to our kernel.

And now, here's the kernel code itself:

```
__global__ void kernel( unsigned char *ptr, int ticks ) {
    // map from threadIdx/BlockIdx to pixel position
    int x = threadIdx.x + blockIdx.x * blockDim.x;
    int y = threadIdx.y + blockIdx.y * blockDim.y;
    int offset = x + y * blockDim.x * gridDim.x;

    // now calculate the value at that position
    float fx = x - DIM/2;
    float fy = y - DIM/2;
    float d = sqrtf( fx * fx + fy * fy );
unsigned char grey = (unsigned char) (128.0f + 127.0f *
cos(d/10.0f - ticks/7.0f) /
(d/10.0f + 1.0f));
ptr[offset*4 + 0] = grey;
ptr[offset*4 + 1] = grey;
ptr[offset*4 + 2] = grey;
ptr[offset*4 + 3] = 255;
}
```

The first three are the most important lines in the kernel.

```
int x = threadIdx.x + blockIdx.x * blockDim.x;
int y = threadIdx.y + blockIdx.y * blockDim.y;
int offset = x + y * blockDim.x * gridDim.x;
```

In these lines, each thread takes its index within its block as well as the index of its block within the grid, and it translates this into a unique (x,y) index within the image. So when the thread at index (3, 5) in block (12, 8) begins executing, it knows that there are 12 entire blocks to the left of it and 8 entire blocks above it. Within its block, the thread at (3, 5) has three threads to the left and five above it. Because there are 16 threads per block, this means the thread in question has the following:

3 threads + 12 blocks * 16 threads/block = 195 threads to the left of it

5 threads + 8 blocks * 16 threads/block = 128 threads above it

This computation is identical to the computation of x and y in the first two lines and is how we map the thread and block indices to image coordinates. Then we simply linearize these x and y values to get an offset into the output buffer. Again, this is identical to what we did in the “GPU Sums of a Longer Vector” and “GPU Sums of Arbitrarily Long Vectors” sections.

```
int offset = x + y * blockDim.x * gridDim.x;
```

Since we know which (x,y) pixel in the image the thread should compute and we know the time at which it needs to compute this value, we can compute any function of (x, y, t) and store this value in the output buffer. In this case, the function produces a time-varying sinusoidal "ripple."

```
float fx = x - DIM/2;
float fy = y - DIM/2;
float d = sqrtf( fx * fx + fy * fy );
unsigned char grey = (unsigned char)(128.0f + 127.0f *
cos( d/10.0f - ticks/7.0f ) /
(d/10.0f + 1.0f) );
```

We recommend that you not get too hung up on the computation of grey. It's essentially just a 2D function of time that makes a nice rippling effect when it's animated. A screenshot of one frame should look something like Figure 5.3.

![](img/d5750f02645080d2a91292047fbe0f98_94_0.png)

Figure 5.3 A screenshot from the GPU ripple example

## 5.3 Shared Memory and Synchronization

So far, the motivation for splitting blocks into threads was simply one of working around hardware limitations to the number of blocks we can have in flight. This is fairly weak motivation, because this could easily be done behind the scenes by the CUDA runtime. Fortunately, there are other reasons one might want to split a block into threads.

CUDA C makes available a region of memory that we call _shared memory_. This region of memory brings along with it another extension to the C language akin to `__device__` and `__global__`. As a programmer, you can modify your variable declarations with the CUDA C keyword `__shared__` to make this variable resident in shared memory. But what’s the point?

We’re glad you asked. The CUDA C compiler treats variables in shared memory differently than typical variables. It creates a copy of the variable for each block that you launch on the GPU. Every thread in that block shares the memory, but threads cannot see or modify a copy of this variable that is seen within other blocks. This provides an excellent means of by which threads within a block can communicate and collaborate on computations. Furthermore, shared memory buffers reside physically on the GPU as opposed to residing in off-chip DRAM. Because of this, the latency to access shared memory tends to be far lower than typical buffers, making shared memory effective as a per-block, software-managed cache or scratchpad.

The prospect of communication between threads should excite you. It excites us, too. But nothing in life is free, and interthread communication is no exception. If we expect to communicate between threads, we also need a mechanism for synchronizing between threads. For example, if thread A writes a value to shared memory and we want thread B to do something with this value, we can’t have thread B start its work until we know the write from thread A is complete. Without synchronization, we have created a race condition where the correctness of the execution results depends on the nondeterministic details of the hardware.

Let’s take a look at an example that uses these features.
