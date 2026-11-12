

请注意，我们的起点与那些输出图像的示例完全相同。不过，线程计算的不是像素的颜色，而是模拟网格单元的温度。尽管如此，它们首先会将自己的 `threadIdx` 和 `blockIdx` 转换为 `x`、`y` 和 `offset`。到现在为止，你可能已经能在睡梦中背诵这些代码行了（虽然为了你好，我们希望你并没有真的在睡梦中背诵它们）。

接下来，我们确定左、右、上、下邻居的偏移量，以便读取这些单元的温度。我们需要这些值来计算当前单元的更新温度。这里唯一的复杂之处在于，我们需要调整边界上的索引，以便边缘周围的单元不会环绕。最后，在高亮显示的行中，我们执行方程 7.2 中的更新，将旧温度与该温度及其邻居单元温度的缩放差值相加。

## 7.3.3 模拟动画

代码的其余部分主要设置网格，然后显示热图的动画输出。我们现在来逐行讲解这段代码：

```cpp
#include "cuda.h"
#include "../common/book.h"
#include "../common/cpu_anim.h"

#define DIM 1024
#define PI 3.1415926535897932f
#define MAX_TEMP 1.0f
#define MIN_TEMP 0.0001f
#define SPEED   0.25f

// globals needed by the update routine
struct DataBlock {
    unsigned char     *output_bitmap;
    float             *dev_inSrc;
    float             *dev_outSrc;
    float             *dev_constSrc;
    CPUAnimBitmap  *bitmap;
    cudaEvent_t      start, stop;
    float            totalTime;
    float            frames;
};

void anim_gpu( DataBlock *d, int ticks ) {
    HANDLE_ERROR( cudaEventRecord( d->start, 0 ) );
    dim3     blocks( DIM/16, DIM/16 );
    dim3     threads( 16, 16 );
    CPUBitmap *bitmap = d->bitmap;

    for ( int i=0; i<90; i++ ) {
        copy_const_kernel<<<blocks,threads>>>( d->dev_inSrc,
                                               d->dev_constSrc );
        blend_kernel<<<blocks,threads>>>( d->dev_outSrc,
                                          d->dev_inSrc );
        swap( d->dev_inSrc, d->dev_outSrc );
    }

    float_to_color<<<blocks,threads>>>( d->output_bitmap,
                                         d->dev_inSrc );

    HANDLE_ERROR( cudaMemcpy( bitmap->get_ptr(),
                              d->output_bitmap,
                              bitmap->image_size(),
                              cudaMemcpyDeviceToHost ) );

    HANDLE_ERROR( cudaEventRecord( d->stop, 0 ) );
    HANDLE_ERROR( cudaEventSynchronize( d->stop ) );
    float   elapsedTime;
    HANDLE_ERROR( cudaEventElapsedTime( &elapsedTime,
                                        d->start, d->stop ) );

    d->totalTime += elapsedTime;
    ++d->frames;

    printf( "Average Time per frame:  %3.1f ms\n",
            d->totalTime/d->frames );
}

void anim_exit( DataBlock *d ) {
    cudaFree( d->dev_inSrc );
    cudaFree( d->dev_outSrc );
    cudaFree( d->dev_constSrc );

    HANDLE_ERROR( cudaEventDestroy( d->start ) );
    HANDLE_ERROR( cudaEventDestroy( d->stop ) );
}
```

我们为代码配备了基于事件的计时，与上一章光线追踪示例中所做的一样。计时代码的作用与之前相同。由于我们将致力于加速初始实现，因此我们建立了一种机制，用于测量性能并让自己确信已取得成功。

动画框架会在每一帧调用函数 `anim_gpu()`。该函数的参数是一个指向 `DataBlock` 的指针以及动画已经过的 tick 数。与动画示例一样，我们使用 256 个线程的块，并将其组织成 16 x 16 的二维网格。`anim_gpu()` 中 `for()` 循环的每次迭代都会计算模拟的一个时间步，如第 7.2.2 节开头所述的三步算法“计算温度更新”中所述。由于 `DataBlock` 包含加热器的常量缓冲区以及上一个时间步的输出，它封装了动画的整个状态，因此 `anim_gpu()` 实际上不需要在任何地方使用 `ticks` 的值。

你会发现，我们选择每帧执行 90 个时间步。这个数字并非神奇，而是通过一定程度的实验确定的，旨在权衡每个时间步都下载位图图像与每帧计算过多时间步（导致动画卡顿）之间的合理折衷。如果你更关心获得每个模拟步骤的输出，而不是实时动画化结果，则可以将其更改为每帧仅计算一个步骤。

计算完自上一帧以来的 90 个时间步后，`anim_gpu()` 准备将当前动画的位图帧复制回 CPU。由于 `for()` 循环会交换输入和输出，我们首先交换输入和输出缓冲区，以便输出实际上包含第 90 个时间步的输出。我们使用内核 `float_to_color()` 将温度转换为颜色，然后使用 `cudaMemcpy()` 将生成的图像复制回 CPU，并指定复制方向为 `cudaMemcpyDeviceToHost`。最后，为准备下一组时间步，我们将输出缓冲区换回输入缓冲区，因为它将作为下一个时间步的输入。

```cpp
int main( void ) {
    DataBlock data;
    CPUAnimBitmap bitmap( DIM, DIM, &data );
    data.bitmap = &bitmap;
    data.total_time = 0;
    data.frames = 0;
    HANDLE_ERROR( cudaEventCreate( &data.start ) );
    HANDLE_ERROR( cudaEventCreate( &data.stop ) );

    HANDLE_ERROR( cudaMalloc( (void**)&data.output_bitmap,
                              bitmap.image_size() ) );

    // assume float == 4 chars in size (i.e., rgba)
    HANDLE_ERROR( cudaMalloc( (void**)&data.dev_inSrc,
                              bitmap.image_size() ) );
    HANDLE_ERROR( cudaMalloc( (void**)&data.dev_outSrc,
                              bitmap.image_size() ) );
    HANDLE_ERROR( cudaMalloc( (void**)&data.dev_constSrc,
                              bitmap.image_size() ) );

    float *temp = (float*)malloc( bitmap.image_size() );
    for (int i=0; i<DIM*DIM; i++) {
        temp[i] = 0;
        int x = i % DIM;
        int y = i / DIM;
        if ((x<300) && (x<600) && (y>310) && (y<601))
            temp[i] = MAX_TEMP;
    }
}
temp[DIM*100+100] = (MAX_TEMP + MIN_TEMP)/2;
temp[DIM*700+100] = MIN_TEMP;
temp[DIM*300+300] = MIN_TEMP;
temp[DIM*200+700] = MIN_TEMP;
for (int y=800; y<900; y++) {
    for (int x=400; x<500; x++) {
    temp[x+y*DIM] = MIN_TEMP;
    }
}
HANDLE_ERROR( cudaMemcpy( data.dev_constSrc, temp,
                        bitmap.image_size(),
                        cudaMemcpyHostToDevice ) );
for (int y=800; y<DIM; y++) {
    for (int x=0; x<200; x++) {
    temp[x+y*DIM] = MAX_TEMP;
    }
}
HANDLE_ERROR( cudaMemcpy( data.dev_inSrc, temp,
                        bitmap.image_size(),
                        cudaMemcpyHostToDevice ) );
free( temp );
bitmap.anim_and_exit( (void (*)(void*,int))anim_gpu,
                    (void (*)(void*))anim_exit );
}
```

图 7.4 展示了输出可能呈现的示例。你会在图像中注意到一些“加热器”，它们看起来像是像素大小的岛屿，破坏了温度分布的连续性。

## 7.3.4 使用纹理内存

执行每个步骤的温度更新所需的内存访问模式具有相当大的空间局部性。如前所述，这正是 GPU 纹理内存旨在加速的那种访问模式。

![](img/d5750f02645080d2a91292047fbe0f98_146_0.png)

图 7.4 动画热传递模拟的截图

鉴于我们想要使用纹理内存，我们需要了解如何操作。

首先，我们需要将输入声明为纹理引用。由于我们的温度数据是浮点型，因此我们将使用浮点纹理的引用。

```cpp
// these exist on the GPU side
texture<float> texConstSrc;
texture<float> texIn;
texture<float> texOut;
```

下一个主要区别是，在为这三个缓冲区分配 GPU 内存后，我们需要使用 `cudaBindTexture()` 将引用绑定到内存缓冲区。这基本上告诉 CUDA 运行时两件事：

- 我们打算将指定的缓冲区用作纹理。
- 我们打算将指定的纹理引用用作纹理的“名称”。

