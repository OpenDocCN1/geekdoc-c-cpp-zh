```
glDrawPixels( bitmap->x,
bitmap->y,
GL_RGBA,
GL_UNSIGNED_BYTE,
bitmap->pixels );
```

We remarked in the first example of this chapter that you may have previously
seen calls to glDrawPixels() ) with a buffer pointer as the last argument.
Well, if you hadn't before, you have now. This call in the Draw() routine of
CPUMemBitmap triggers a copy of the CPU buffer in bitmap->pixels to the
GPU for rendering. To do this, the CPU needs to stop what it's doing and initiate
a copy onto the GPU for every frame. This requires synchronization between the
CPU and GPU and additional latency to initiate and complete a transfer over the
PCI Express bus. Since the call to glDrawPixels() expects a host pointer in
the last argument, this also means that after generating a frame of image data
with a CUDA C kernel, our Chapter 5 ripple application needed to copy the frame
from the GPU to the CPU with a cudaMemcpy().

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

Taken together, these facts mean that our original GPU ripple application
was more than a little silly. We used CUDA C to compute image values for our
rendering in each frame, but after the computations were done, we copied the
buffer to the CPU, which then copied the buffer back to the GPU for display. This
means that we introduced unnecessary data transfers between the host and