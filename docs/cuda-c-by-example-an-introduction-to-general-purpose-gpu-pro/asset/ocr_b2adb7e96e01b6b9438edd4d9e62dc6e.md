Since kernel() is a CUDA C function that generates image data, all that remains is writing a host function that will be used as a callback in the idle_func() member of GPUAnimBitmap. For our current application, all this function does is launch the CUDA C kernel:

```
void generate_frame( uchar4 *pixels, void*, int ticks ) {
    dim3  grids(DIM/16,DIM/16);
    dim3  threads(16,16);
    kernel<<<grids,threads>>>( pixels, ticks );
}
```

That's basically everything we need, since all of the heavy lifting was done in the GPUAnimBitmap structure. To get this party started, we just create a GPUAnimBitmap and register our animation callback function, generate_frame().

```
int main( void ) {
    GPUAnimBitmap  bitmap( DIM, DIM, NULL );

    bitmap.anim_and_exit(
        (void (*)(uchar4*,void*,int))generate_frame, NULL );
}
```

# 8.4 Heat Transfer with Graphics Interop

So, what has been the point of doing all of this? If you look at the internals of the CPUAnimBitmap, the structure we used for previous animation examples, we would see that it works almost exactly like the rendering code in Section 8.1: Graphics Interoperation.

Almost.

The key difference between the CPUAnimBitmap and the previous example is buried in the call to glDrawPixels().