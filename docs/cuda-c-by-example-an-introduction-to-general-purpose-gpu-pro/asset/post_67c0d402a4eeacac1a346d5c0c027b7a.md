
the device that stood between us and maximum performance. Let's revisit a compute-intensive animation application that might see its performance improve by migrating it to use graphics interoperation for its rendering.

If you recall the previous chapter's heat simulation application, you will remember that it also used CUDAAnimBitmap in order to display the output of its simulation computations. We will modify this application to use our newly implemented GPUAnimBitmap structure and look at how the resulting performance changes. As with the ripple example, our GPUAnimBitmap is almost a perfect drop-in replacement for CPUAnimBitmap, with the exception of the unsigned char to uchar4 change. So, the signature of our animation routine changes in order to accommodate this shift in data types.

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

Since the `float_to_color()` kernel is the only function that actually uses the outputBitmap, it's the only other function that needs modification as a result of our shift to uchar4. This function was simply considered utility code in the previous chapter, and we will continue to consider it utility code. However, we have overloaded this function and included both `unsigned char` and `uchar4` versions in book.h. You will notice that the differences between these functions are identical to the differences between kernel () in the CPU-animated and GPU-animated versions of GPU ripple. Most of the code for the `float_to_color()` kernels has been omitted for clarity, but we encourage you to consult book.h if you're dying to see the details.

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

Outside of these changes, the only major difference is in the change from CPUAnimBitmap to GPUAnimBitmap to perform animation.

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

Although it might be instructive to take a glance at the rest of this enhanced heat simulation application, it is not sufficiently different from the previous chapter's version to warrant more description. The important component is answering the question, how does performance change now that we've completely migrated the application to the GPU? Without having to copy every frame back to the host for display, the situation should be much happier than it was previously.

So, exactly how much better is it to use the graphics interoperability to perform the rendering? Previously, the heat transfer example consumed about 25.3ms per frame on our GeForce GTX 285–based test machine. After converting the application to use graphics interoperability, this drops by 15 percent to 21.6ms per frame. The net result is that our rendering loop is 15 percent faster and no longer requires intervention from the host every time we want to display a frame. That's not bad for a day's work!

## 8.5 DirectX Interoperability

Although we've looked only at examples that use interoperation with the OpenGL rendering system, DirectX interoperation is nearly identical. You will still use a cudaGraphicsResource to refer to buffers that you share between DirectX and CUDA, and you will still use calls to cudaGraphicsMapResources() and cudaGraphicsResourceGetMappedPointer() to retrieve CUDA-friendly pointers to these shared resources.

For the most part, the calls that differ between OpenGL and DirectX interoperability have embarrassingly simple translations to DirectX. For example, rather than calling cudaGLSetGLDevice(), we call cudaD3D9SetDirect3DDevice() to specify that a CUDA device should be enabled for Direct3D 9.0 interoperability.

Likewise, cudaD3D10SetDirect3DDevice() enables a device for Direct3D 10 interoperation and cudaD3D11SetDirect3DDevice() for Direct3D 11.

The details of DirectX interoperability probably will not surprise you if you've worked through this chapter's OpenGL examples. But if you want to use DirectX interoperation and want a small project to get started, we suggest that you migrate this chapter's examples to use DirectX. To get started, we recommend consulting the NVIDIA CUDA Programming Guide for a reference on the API and taking a look at the GPU Computing SDK code samples on DirectX interoperability.

## 8.6 Chapter Review

Although much of this book has been devoted to using the GPU for parallel, general-purpose computing, we can't forget the GPU's successful day job as a rendering engine. Many applications require or would benefit from the use of standard computer graphics rendering. Since the GPU is master of the rendering domain, all that stood between us and the exploitation of these resources was a lack of understanding of the mechanics in convincing the CUDA runtime and graphics drivers to cooperate. Now that we have seen how this is done, we no longer need the host to intervene in displaying the graphical results of our computations. This simultaneously accelerates the application's rendering loop and frees the host to perform other computations in the meantime. Otherwise, if there are no other computations to be performed, it leaves our system more responsive to other events or applications.

There are many other ways to use graphics interoperability that we left unexplored. We looked primarily at using a CUDA C kernel to write into a pixel buffer object for display in a window. This image data can also be used as a texture that can be applied to any surface in the scene. In addition to modifying pixel buffer objects, you can also share vertex buffer objects between CUDA and the graphics engine. Among other things, this allows you to write CUDA C kernels that perform collision detection between objects or compute vertex displacement maps to be used to render objects or surfaces that interact with the user or their surroundings. If you're interested in computer graphics, CUDA C's graphics interoperability API enables a slew of new possibilities for your applications!
