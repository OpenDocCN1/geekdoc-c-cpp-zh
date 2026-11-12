

本书的预期范围。相反，本章旨在聚焦于CUDA C及其提供的将其集成到图形应用程序中的设施。如果您不熟悉OpenGL或DirectX，不太可能从本章中获益良多，可能希望跳到下一章。

## 8.1 章节目标

在本章学习过程中，您将完成以下任务：

- 您将了解什么是*图形互操作性*以及为何可能使用它。
- 您将了解如何为图形互操作性设置CUDA设备。
- 您将了解如何在CUDA C内核和OpenGL渲染之间共享数据。

## 8.2 图形互操作

为了演示图形与CUDA C之间互操作的机制，我们将编写一个分两步执行的应用程序。第一步使用CUDA C内核生成图像数据。第二步，应用程序将此数据传递给OpenGL驱动程序进行渲染。为了实现这一点，我们将使用前几章中看到的大部分CUDA C，以及一些OpenGL和GLUT调用。

要启动我们的应用程序，我们包含相关的GLUT和CUDA头文件，以确保定义了正确的函数和枚举。我们还定义应用程序计划渲染的窗口大小。在512 x 512像素下，我们将进行相对较小的绘图。

```
#define GL_GLEXT_PROTOTYPES
#include "GL/glut.h"
#include "cuda.h"
#include "cuda_gl_interop.h"
#include "../common/book.h"
#include "../common/cpu_bitmap.h"

#define DIM 512
```

此外，我们声明两个全局变量，用于存储我们打算在OpenGL和数据之间共享的数据的句柄。我们稍后将看到如何使用这两个变量，但它们将存储同一缓冲区的不同句柄。我们需要两个独立的变量，因为OpenGL和CUDA都会为缓冲区有不同的“名称”。变量bufferObj将是OpenGL对数据的名称，变量resource将是CUDA C对它的名称。

```
GLuint bufferObj;
cudaGraphicsResource *resource;
```

现在让我们来看看实际的应用程序。我们要做的第一件事是选择一个用于运行应用程序的CUDA设备。在许多系统中，这并不是一个复杂的过程，因为它们通常只包含一个支持CUDA的GPU。然而，越来越多的系统包含多个支持CUDA的GPU，因此我们需要一种方法来选择其中一个。幸运的是，CUDA运行时为我们提供了这样的设施。

```
int main( int argc, char **argv ) {
    cudaDeviceProp prop;
    int dev;
    memset( &prop, 0, sizeof( cudaDeviceProp ) );
    prop.major = 1;
    prop.minor = 0;
    HANDLE_ERROR( cudaChooseDevice( &dev, &prop ) );
}
```

您可能记得我们在第3章中见过cudaChooseDevice()，但由于它是一个次要的点，我们现在将再次回顾它。基本上，这段代码告诉运行时选择任何计算能力为1.0版本或更高的GPU。它通过首先创建并清除一个cudaDeviceProp结构，然后将其主版本设置为1、次版本设置为0来实现这一点。它将此信息传递给cudaChooseDevice()，该函数指示运行时选择系统中满足cudaDeviceProp结构指定约束的GPU。在下一章中，我们将更多地了解GPU的计算能力是什么意思，但目前可以说它大致指示GPU支持的功能。所有支持CUDA的GPU至少具有计算能力1.0，因此此调用的净效果是运行时将选择任何支持CUDA的设备，并在变量dev中返回该设备的标识符。不能保证此设备是最佳或最快的GPU，也不能保证该设备在CUDA运行时的不同版本中将是同一个GPU。

如果设备选择的结果看起来如此令人失望，为什么我们要费尽周折填充cudaDeviceProp结构并调用cudaChooseDevice()来获取有效的设备ID？此外，我们以前从未费心处理这些琐事，为什么现在要处理？这些是很好的问题。事实证明，我们需要知道CUDA设备ID，以便告诉CUDA运行时我们打算将该设备用于CUDA和OpenGL。我们通过调用cudaGLSetGLDevice()来实现这一点，传递从cudaChooseDevice()获得的设备ID dev：

```
HANDLE_ERROR( cudaGLSetGLDevice( dev ) );
```

在CUDA运行时初始化之后，我们可以通过调用我们的GL实用工具包(GLUT)设置函数来初始化OpenGL驱动程序。如果您以前使用过GLUT，这一系列调用应该对您来说相对熟悉：

```
// these GLUT calls need to be made before the other GL calls
glutInit( &argc, argv );
glutInitDisplayMode( GLUT_DOUBLE | GLUT_RGBA );
glutInitWindowSize( DIM, DIM );
glutCreateWindow( "bitmap" );
```

在main()的这个阶段，我们通过调用cudaGLSetGLDevice()已准备好让CUDA运行时与OpenGL驱动程序良好协作。然后我们初始化了GLUT并创建了一个名为"bitmap"的窗口来绘制我们的结果。现在我们可以开始实际的OpenGL互操作了！

共享数据缓冲区是CUDA C内核与OpenGL渲染之间互操作的关键组件。要在OpenGL和CUDA之间传递数据，我们首先需要创建一个可以同时与两个API一起使用的缓冲区。我们通过在OpenGL中创建一个像素缓冲区对象并将句柄存储在我们的全局变量GLuint bufferObj中来开始此过程：

```
glGenBuffers( 1, &bufferObj );
glBindBuffer( GL_PIXEL_UNPACK_BUFFER_ARB, bufferObj );
glBufferData( GL_PIXEL_UNPACK_BUFFER_ARB, DIM * DIM * 4,
NULL, GL_DYNAMIC_DRAW_ARB );
```

如果您以前从未在OpenGL中使用过像素缓冲区对象(PBO)，通常会通过以下三个步骤创建一个：首先，我们使用glGenBuffers()生成一个缓冲区句柄。然后，我们使用glBindBuffer()将句柄绑定到像素缓冲区。最后，我们请求OpenGL驱动程序使用glBufferData()分配一个缓冲区。在此示例中，我们请求一个缓冲区来保存DIM x DIM个32位值，并使用枚举GL_DYNAMIC_DRAW_ARB指示该缓冲区将由应用程序反复修改。由于我们没有数据预加载到缓冲区中，我们将NULL作为glBufferData()的倒数第二个参数传递。

在设置图形互操作性的过程中，剩下的就是通知CUDA运行时我们打算将名为bufferObj的OpenGL缓冲区与CUDA共享。我们通过将bufferObj作为图形资源注册到CUDA运行时来实现这一点。

```
HANDLE_ERROR(
    cudaGraphicsGLRegisterBuffer( &resource,
                                      bufferObj,
                                      cudaGraphicsMapFlagsNone )
);
```

我们通过调用cudaGraphicsGLRegisterBuffer()向CUDA运行时指定我们打算将OpenGL PBO bufferObj同时用于OpenGL和CUDA。CUDA运行时在变量resource中返回一个CUDA友好的缓冲区句柄。此句柄将用于在后续对CUDA运行时的调用中引用bufferObj。

标志cudaGraphicsMapFlagsNone指定我们不想为该缓冲区指定任何特定行为，尽管我们可以选择使用cudaGraphicsMapFlagsReadOnly指定缓冲区将是只读的。我们也可以使用cudaGraphicsMapFlagsWriteDiscard指定之前的内容将被丢弃，使缓冲区本质上是只写的。这些标志允许CUDA和OpenGL驱动程序为具有受限访问模式的缓冲区优化硬件设置，尽管它们不是必须设置的。

实际上，调用glBufferData()请求OpenGL驱动程序分配一个足够大的缓冲区来容纳DIM x DIM个32位值。在后续的OpenGL调用中，我们将使用句柄bufferObj引用此缓冲区，而在CUDA运行时调用中，我们将使用指针resource引用此缓冲区。由于我们希望从CUDA C内核读取和写入此缓冲区，我们将需要不仅仅是对象的句柄。我们将需要设备内存中的一个实际地址，该地址可以

