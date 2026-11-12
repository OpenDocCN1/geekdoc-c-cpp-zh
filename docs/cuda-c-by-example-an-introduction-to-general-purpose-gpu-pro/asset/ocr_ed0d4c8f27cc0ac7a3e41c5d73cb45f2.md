Although this may not be the end of the world, your application might be computing more important values.

Instead, we need to add a synchronization point between the write to shared memory and the subsequent read from it.

```
shared[threadIdx.x][threadIdx.y] =
  255 * (sinf(x*2.0f*PI / period) + 1.0f) *
  (sinf(y*2.0f*PI / period) + 1.0f) / 4.0f;

__syncthreads();

ptr[offset*4 + 0] = 0;
ptr[offset*4 + 1] = shared[15-threadIdx.x][15-threadIdx.y];
ptr[offset*4 + 2] = 0;
ptr[offset*4 + 3] = 255;
}
```

With this __syncthreads() in place, we then get a far more predictable [and aesthetically pleasing] result, as shown in Figure 5.6.

![](bbox=[0.263, 0.563, 0.648, 0.872])

Figure 5.6 A screenshot after adding the correct synchronization