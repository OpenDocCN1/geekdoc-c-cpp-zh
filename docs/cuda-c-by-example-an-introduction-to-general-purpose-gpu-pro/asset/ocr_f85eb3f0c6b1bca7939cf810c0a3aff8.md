```
// clean up memory allocated on the GPU
void anim_exit( DataBlock *d ) {
 cudaUnbindTexture( texIn );
 cudaUnbindTexture( texOut );
 cudaUnbindTexture( texConstSrc );
 cudaFree( d->dev_inSrc );
 cudaFree( d->dev_outSrc );
 cudaFree( d->dev_constSrc );

 HANDLE_ERROR( cudaEventDestroy( d->start ) );
 HANDLE_ERROR( cudaEventDestroy( d->stop ) );
}
```

# 7.3.5 USING TWO-DIMENSIONAL TEXTURE MEMORY

Toward the beginning of this book, we mentioned how some problems have two-dimensional domains, and therefore it can be convenient to use two-dimensional blocks and grids at times. The same is true for texture memory. There are many cases when having a two-dimensional memory region can be useful, a claim that should come as no surprise to anyone familiar with multidimensional arrays in standard C. Let's look at how we can modify our heat transfer application to use two-dimensional textures.

First, our texture reference declarations change. If unspecified, texture references are one-dimensional by default, so we add a dimensionality argument of 2 in order to declare two-dimensional textures.

```
texture<float,2> texConstSrc;
texture<float,2> texIn;
texture<float,2> texOut;
```

The simplification promised by converting to two-dimensional textures comes in the blend_kernel() method. Although we need to change our texIDFetch()