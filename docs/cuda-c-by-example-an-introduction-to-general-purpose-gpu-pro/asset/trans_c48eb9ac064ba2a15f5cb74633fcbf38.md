

阻碍我们获得最大性能的设备。让我们重新审视一个计算密集型动画应用程序，它可能通过迁移到使用图形互操作进行渲染来提升性能。

如果你还记得上一章的热模拟应用程序，你会记得它也使用 CUDAAnimBitmap 来显示其模拟计算的输出。我们将修改此应用程序以使用我们新实现的 GPUAnimBitmap 结构，并查看由此产生的性能变化。与波纹示例一样，我们的 GPUAnimBitmap 几乎是 CPUAnimBitmap 的完美即插即用替代品，除了 unsigned char 到 uchar4 的更改之外。因此，我们的动画例程的签名会发生变化，以适应这种数据类型的转变。

```cpp
void anim_gpu( uchar4* outputBitmap, DataBlock *d, int ticks ) {
    HANDLE_ERROR( cudaEventRecord( d->start, 0 ) );
    dim3 blocks(DIM/16,DIM/16);
    dim3 threads(16,16);
    // since tex is global and bound, we have to use a flag to
    // select which is in/out per iteration
    volatile bool dstOut = true;
    for (int i=0; i<90; i++) {
        float *in, *out;
        if (dstOut) {
            in = d->dev_inSrc;
            out = d->dev_outSrc;
        } else {
            out = d->dev_inSrc;
            in = d->dev_outSrc;
        }
        copy_const_kernel<<<blocks,threads>>>( in );
        blend_kernel<<<blocks,threads>>>( out, dstOut );
        dstOut = !dstOut;
    }
    float_to_color<<<blocks,threads>>>( outputBitmap,
        d->dev_inSrc );
}
```

```cpp
HANDLE_ERROR( cudaEventRecord( d->stop, 0 ) );
HANDLE_ERROR( cudaEventSynchronize( d->stop ) );
float   elapsedTime;
HANDLE_ERROR( cudaEventElapsedTime( &elapsedTime,
                                        d->start, d->stop ) );
d->totalTime +=  elapsedTime;
++d->frames;
printf( "Average Time per frame:  %3.1f ms\n",
        d->totalTime/d->frames );
}
```

由于 `float_to_color()` 内核是实际使用 outputBitmap 的唯一函数，因此它是我们转向 uchar4 后唯一需要修改的其他函数。在上一章中，这个函数仅被视为实用工具代码，我们将继续将其视为实用工具代码。但是，我们重载了这个函数，并在 book.h 中包含了 `unsigned char` 和 `uchar4` 两个版本。你会注意到，这些函数之间的差异与 GPU ripple 的 CPU 动画和 GPU 动画版本之间 kernel () 的差异相同。为了清晰起见，`float_to_color()` 内核的大部分代码已被省略，但如果你急于查看详细信息，我们鼓励你查阅 book.h。

```cpp
__global__ void float_to_color( unsigned char *optr,
                                    const float  *outSrc ) {
// convert floating-point value to 4-component color
optr[offset*4 + 0] = value( m1, m2, h+120 );
optr[offset*4 + 1] = value( m1, m2, h     );
optr[offset*4 + 2] = value( m1, m2, h -120 );
optr[offset*4 + 3] = 255;
}
```

```cpp
__global__ void float_to_color( uchar4 *optr,
                                 const float *outSrc ) {
  // convert floating-point value to 4-component color

  optr[offset].x = value( m1, m2, h-120 );
  optr[offset].y = value( m1, m2, h );
  optr[offset].z = value( m1, m2, h -120 );
  optr[offset].w = 255;
}
```

除了这些更改之外，唯一的主要区别在于从 CPUAnimBitmap 更改为 GPUAnimBitmap 以执行动画。

```cpp
int main( void ) {
  DataBlock data;

  GPUAnimBitmap  bitmap( DIM, DIM, &data );

  data.totalTime = 0;
  data.frames = 0;

  HANDLE_ERROR( cudaEventCreate( &data.start ) );
  HANDLE_ERROR( cudaEventCreate( &data.stop ) );

  int imageSize = bitmap.image_size();

  // assume float == 4 chars in size (i.e., rgba)
  HANDLE_ERROR( cudaMalloc( (void**)&data.dev_inSrc,
                            imageSize ) );
  HANDLE_ERROR( cudaMalloc( (void**)&data.dev_outSrc,
                            imageSize ) );
  HANDLE_ERROR( cudaMalloc( (void**)&data.dev_constSrc,
                            imageSize ) );

  HANDLE_ERROR( cudaBindTexture( NULL, texConstSrc,
                                 data.dev_constSrc,
                                 imageSize ) );

  HANDLE_ERROR( cudaBindTexture( NULL, texIn,
                                data.dev_inSrc,
                                imageSize ) );

  HANDLE_ERROR( cudaBindTexture( NULL, texOut,
                                data.dev_outSrc,
                                imageSize ) );

  // initialize the constant data
  float *temp = (float*)malloc( imageSize );
  for (int i = 0; i < DIM*DIM; i++) {
      temp[i] = 0;
      int x = i % DIM;
      int y = i / DIM;
      if ((x>300) && (x<600) && (y>310) && (y<601))
          temp[i] = MAX_TEMP;
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
                           imageSize,
                           cudaMemcpyHostToDevice ) );

  // initialize the input data
  for (int y=800; y<DIM; y++) {
      for (int x=0; x<200; x++) {
          temp[x+y*DIM] = MAX_TEMP;
      }
  }

  HANDLE_ERROR( cudaMemcpy( data.dev_inSrc, temp,
                           imageSize,
                           cudaMemcpyHostToDevice ) );

  free( temp );

  bitmap.anim_and_exit( (void (*)(uchar4*,void*,int))anim_gpu,
                        (void (*)(void*))anim_exit );
}
```

虽然浏览这个增强版热模拟应用程序的其余部分可能很有启发性，但它与上一章的版本没有足够大的区别，不值得更多描述。重要的是回答这样一个问题：现在我们已将应用程序完全迁移到 GPU，性能会如何变化？无需将每一帧都复制回主机进行显示，情况应该比以前好得多。

那么，使用图形互操作性进行渲染到底好多少呢？以前，热传递示例在我们基于 GeForce GTX 285 的测试机上每帧消耗约 25.3ms。将应用程序转换为使用图形互操作性后，这下降了 15%，降至每帧 21.6ms。净结果是，我们的渲染循环快了 15%，并且每次想要显示一帧时都不再需要主机干预。一天的工作成果还不错！

## 8.5 DirectX 互操作性

虽然我们只查看了使用与 OpenGL 渲染系统互操作的示例，但 DirectX 互操作几乎是一样的。你仍将使用 cudaGraphicsResource 来引用在 DirectX 和 CUDA 之间共享的缓冲区，并且仍将使用 cudaGraphicsMapResources() 和 cudaGraphicsResourceGetMappedPointer() 调用来检索这些共享资源的 CUDA 友好指针。

在大多数情况下，OpenGL 和 DirectX 互操作性之间不同的调用都有尴尬地简单的 DirectX 翻译。例如，我们不再调用 cudaGLSetGLDevice()，而是调用 cudaD3D9SetDirect3DDevice() 以指定应启用 CUDA 设备以进行 Direct3D 9.0 互操作性。

同样，cudaD3D10SetDirect3DDevice() 启用设备以进行 Direct3D 10 互操作，cudaD3D11SetDirect3DDevice() 用于 Direct3D 11。

如果你已经完成了本章的 OpenGL 示例，DirectX 互操作性的细节可能不会让你感到惊讶。但是，如果你想使用 DirectX 互操作并想要一个小项目来入门，我们建议你将本章的示例迁移到 DirectX。要开始，我们建议查阅 NVIDIA CUDA 编程指南作为 API 参考，并查看 GPU Computing SDK 中关于 DirectX 互操作性的代码示例。

## 8.6 章节回顾

虽然本书大部分内容都致力于使用 GPU 进行并行通用计算，但我们不能忘记 GPU 作为渲染引擎的成功日常工作。许多应用程序需要或将受益于使用标准计算机图形渲染。由于 GPU 是渲染领域的主宰，阻碍我们利用这些资源的唯一东西是缺乏对说服 CUDA 运行时和图形驱动程序合作的机制的理解。现在我们已经知道了如何做到这一点，我们不再需要主机干预来显示我们计算的图形结果。这同时加速了应用程序的渲染循环，并使主机能够同时执行其他计算。否则，如果没有其他计算要执行，它会使我们的系统对其他事件或应用程序更加响应。

还有许多其他使用图形互操作性的方法我们未加探索。我们主要研究了使用 CUDA C 内核写入像素缓冲区对象以在窗口中显示。这些图像数据也可以用作可应用于场景中任何表面的纹理。除了修改像素缓冲区对象之外，你还可以在 CUDA 和图形引擎之间共享顶点缓冲区对象。其中，这允许你编写 CUDA C 内核来执行对象之间的碰撞检测或计算顶点位移图，以用于渲染与用户或其周围环境交互的对象或表面。如果你对计算机图形学感兴趣，CUDA C 的图形互操作性 API 为你的应用程序开启了大量新的可能性！

