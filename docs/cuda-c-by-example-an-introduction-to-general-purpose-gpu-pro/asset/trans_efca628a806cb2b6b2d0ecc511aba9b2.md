

```
// first, find a CUDA device and set it to graphic interop
cudaDeviceProp prop;
int dev;
memset( &prop, 0, sizeof( cudaDeviceProp ) );
prop.major = 1;
prop.minor = 0;
HANDLE_ERROR( cudaChooseDevice( &dev, &prop ) );
```

找到兼容的CUDA设备后，我们向CUDA运行时发出重要的
cudaGLSetGLDevice() 调用，以通知它我们打算将 dev 用作与OpenGL进行互操作的设备：

```
cudaGLSetGLDevice( dev );
```

由于我们的框架使用GLUT来创建窗口渲染环境，我们需要初始化GLUT。不幸的是，这有点尴尬，因为glutInit()需要命令行参数来传递给窗口系统。由于我们没有想要传递的参数，我们希望简单地指定零个命令行参数。不幸的是，某些版本的GLUT存在一个bug，当给定零个参数时会导致应用程序崩溃。因此，我们诱使GLUT认为我们正在传递一个参数，结果一切顺利。

```
int     c=1;
char   *foo = "name";
glutInit( &c, &foo );
```

我们继续像之前示例中一样初始化GLUT。我们创建一个用于渲染的窗口，并使用字符串"bitmap"指定标题。如果您想给窗口起一个更有趣的名字，尽管来吧。

```
glutInitDisplayMode( GLUT_DOUBLE | GLUT_RGBA );
glutInitWindowSize( width, height );
glutCreateWindow( "bitmap" );
```

接下来，我们请求OpenGL驱动程序分配一个缓冲区句柄，并立即将其绑定到 `GL_PIXEL_UNPACK_BUFFER_ARB` 目标，以确保未来对 `glDrawPixels()` 的调用将绘制到我们的互操作缓冲区：

```
glGenBuffers( 1, &bufferObj );
glBindBuffer( GL_PIXEL_UNPACK_BUFFER_ARB, bufferObj );
```

最后，但绝非不重要的是，我们请求OpenGL驱动程序为我们分配一块GPU内存区域。完成此操作后，我们将此缓冲区告知CUDA运行时，并通过使用cudaGraphicsGLRegisterBuffer()注册bufferObj来为此缓冲区请求一个CUDA名称：

```
glBufferData( GL_PIXEL_UNPACK_BUFFER_ARB, width * height * 4,
NULL, GL_DYNAMIC_DRAW_ARB );

HANDLE_ERROR(
cudaGraphicsGLRegisterBuffer( &resource,
bufferObj,
cudaGraphicsMapFlagsNone ) );
}
```

设置好GPUAnimBitmap后，唯一剩下的问题是我们究竟如何执行渲染。渲染的核心将在我们的 `glutIdleFunction()` 中完成。这个函数本质上包含三件事。首先，它映射我们的共享缓冲区并检索该缓冲区的GPU指针：

```
// static method used for GLUT callbacks
static void idle_func( void ) {
static int ticks = 1;
GPUAnimBitmap* bitmap = *(get_bitmap_ptr());
uchar4* devPtr;
size_t size;

HANDLE_ERROR(
cudaGraphicsMapResources( 1, &(bitmap->resource), NULL )
);
HANDLE_ERROR(
cudaGraphicsResourceGetMappedPointer( (void**)&devPtr,
&size,
bitmap->resource )
);
```

其次，它调用用户指定的函数 fAnim()，该函数预计将启动一个CUDA C内核，在 devPtr 处的缓冲区中填充图像数据。

```
bitmap->fAnim( devPtr, bitmap->dataBlock, ticks++ );
```

最后，它取消映射GPU指针，从而释放缓冲区以供OpenGL驱动程序用于渲染。此渲染将通过调用 glutPostRedisplay() 触发。

```
HANDLE_ERROR(
cudaGraphicsUnmapResources( 1,
&(bitmap->resource),
NULL ) );
glutPostRedisplay();
}
```

GPUAnimBitmap结构的其余部分包含重要但有些偏离主题的基础架构代码。如果您对它感兴趣，应该务必检查它。但我们认为，即使您没有时间或兴趣消化GPUAnimBitmap中其余代码，也能够成功继续。

## 8.3.2 GPU涟漪再探

既然我们有了CPUAnimBitmap的GPU版本，就可以继续修改我们的GPU涟漪应用程序，使其完全在GPU上执行动画。首先，我们将包含 gpu_Anim.h，这是我们GPUAnimBitmap实现的所在地。

GPUAnimBitmap。我们还包含了与第5章中检查的几乎相同的内核。

```
#include "../../common/book.h"
#include "../../common/gpu_anim.h"

#define DIM 1024

__global__ void kernel( uchar4 *ptr, int ticks ) {
    // map from threadIdx/BlockIdx to pixel position
    int x = threadIdx.x + blockIdx.x * blockDim.x;
    int y = threadIdx.y + blockIdx.y * blockDim.y;
    int offset = x + y * blockDim.x * gridDim.x;

    // now calculate the value at that position
    float fx = x - DIM/2;
    float fy = y - DIM/2;
    float d = sqrtf( fx * fx + fy * fy );
    unsigned char grey = (unsigned char)(128.0f + 127.0f *
                                         cos(d/10.0f - 
                                         ticks/7.0f) /
                                         (d/10.0f + 1.0f));
    ptr[offset].x = grey;
    ptr[offset].y = grey;
    ptr[offset].z = grey;
    ptr[offset].w = 255;
}
```

我们所做的唯一更改已被突出显示。做出此更改的原因是，OpenGL互操作要求我们的共享表面必须是“图形友好”的。由于实时渲染通常使用四分量红/绿/蓝/Alpha数据元素的数组，我们的目标缓冲区不再像以前那样只是一个 unsigned char 数组。现在，它必须是 uchar4 类型的数组。实际上，在第5章中，我们将缓冲区视为四分量缓冲区，因此总是使用 ptr[offset+4+k] 对其进行索引，其中 k 指示从 0 到 3 的分量。但现在，通过切换到 uchar4 类型，数据的四分量特性变得明确。

由于 kernel() 是生成图像数据的CUDA C函数，剩下要做的就是编写一个主机函数，该函数将用作 GPUAnimBitmap 的 idle_func() 成员中的回调函数。对于我们当前的应用程序，此函数所做的只是启动CUDA C内核：

```
void generate_frame( uchar4 *pixels, void*, int ticks ) {
    dim3  grids(DIM/16,DIM/16);
    dim3  threads(16,16);
    kernel<<<grids,threads>>>( pixels, ticks );
}
```

基本上，我们只需要这些，因为所有繁重的工作都在 GPUAnimBitmap 结构中完成了。要启动这个程序，我们只需创建一个 GPUAnimBitmap 并注册我们的动画回调函数 generate_frame()。

```
int main( void ) {
    GPUAnimBitmap  bitmap( DIM, DIM, NULL );

    bitmap.anim_and_exit(
        (void (*)(uchar4*,void*,int))generate_frame, NULL );
}
```

## 8.4 带图形互操作的热传递

那么，做所有这些的意义何在？如果您查看 CPUAnimBitmap 的内部结构，即我们用于之前动画示例的结构，您会发现它的工作方式几乎与第8.1节：图形互操作中的渲染代码完全相同。

几乎。

CPUAnimBitmap 与之前示例之间的关键区别隐藏在 glDrawPixels() 调用中。

```
glDrawPixels( bitmap->x,
bitmap->y,
GL_RGBA,
GL_UNSIGNED_BYTE,
bitmap->pixels );
```

我们在本章的第一个示例中曾提到，您可能以前见过以缓冲区指针作为最后一个参数的 glDrawPixels() 调用。好吧，如果您以前没有见过，现在见过了。CPUMemBitmap 的 Draw() 例程中的此调用会触发将 bitmap->pixels 中的 CPU 缓冲区复制到 GPU 以进行渲染。为此，CPU 需要停止当前工作，并为每一帧启动一次到 GPU 的复制。这需要 CPU 和 GPU 之间的同步，以及通过 PCI Express 总线启动和完成传输所需的额外延迟。由于 glDrawPixels() 调用在最后一个参数中期望一个主机指针，这也意味着，在使用 CUDA C 内核生成一帧图像数据后，我们第5章的涟漪应用程序需要使用 cudaMemcpy() 将帧从 GPU 复制到 CPU。

```
void generate_frame( DataBlock *d, int ticks ) {
	dim3 grids(DIM/16,DIM/16);
	dim3 threads(16,16);
	kernel<<<grids,threads>>>( d->dev_bitmap, ticks );

	HANDLE_ERROR( cudaMemcpy( d->bitmap->get_ptr(),
		d->dev_bitmap,
		d->bitmap->image_size(),
		cudaMemcpyDeviceToHost ) );
}
```

综合这些事实，我们最初的GPU涟漪应用程序确实有点愚蠢。我们使用CUDA C来计算每帧渲染的图像值，但在计算完成后，我们将缓冲区复制到CPU，然后CPU又将缓冲区复制回GPU以进行显示。这意味着我们在主机和

