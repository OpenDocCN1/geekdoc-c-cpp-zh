
## B.6. Synchronization Functions

```
void __syncthreads();
```

waits until all threads in the thread block have reached this point and all global and shared memory accesses made by these threads prior to __syncthreads() are visible to all threads in the block.

__syncthreads() is used to coordinate communication between the threads of the same block. When some threads within a block access the same addresses in shared or global memory, there are potential read-after-write, write-after-read, or write-after-write hazards for some of these memory accesses. These data hazards can be avoided by synchronizing threads in-between these accesses.

__syncthreads() is allowed in conditional code but only if the conditional evaluates identically across the entire thread block, otherwise the code execution is likely to hang or produce unintended side effects.

Devices of compute capability 2.x and higher support three variations of __syncthreads() described below.

```
int __syncthreads_count(int predicate);
```

is identical to __syncthreads() with the additional feature that it evaluates predicate for all threads of the block and returns the number of threads for which predicate evaluates to non-zero.

```
int __syncthreads_and(int predicate);
```

is identical to __syncthreads() with the additional feature that it evaluates predicate for all threads of the block and returns non-zero if and only if predicate evaluates to non-zero for all of them.

```
int __syncthreads_or(int predicate);
```

is identical to __syncthreads() with the additional feature that it evaluates predicate for all threads of the block and returns non-zero if and only if predicate evaluates to non-zero for any of them.

```
void __syncwarp(unsigned mask=0xFFFFFFFF);
```

will cause the executing thread to wait until all warp lanes named in mask have executed a __syncwarp() (with the same mask) before resuming execution. All non-executed threads named in mask must execute a corresponding __syncwarp() with the same mask, or the result is undefined.

Executing __syncwarp() guarantees memory ordering among threads participating in the barrier. Thus, threads within a warp that wish to communicate via memory can store to memory, execute __syncwarp(), and then safely read values stored by other threads in the warp.

> For .target sm_6x or below, all threads in mask must execute the same __syncwarp() in convergence, and the union of all values in mask must be equal to the active mask. Otherwise, the behavior is undefined.

## B.7. Mathematical Functions

The reference manual lists all C/C++ standard library mathematical functions that are supported in device code and all intrinsic functions that are only supported in device code.

Mathematical Functions provides accuracy information for some of these functions when relevant.

## B.8. Texture Functions

Texture objects are described in Texture Object API.

Texture references are described in Texture Reference API.

Texture fetching is described in Texture Fetching.

### B.8.1. Texture Object API

### B.8.1.1. tex1Dfetch()

```
template<class T>
T tex1Dfetch(cudaTextureObject_t texObj, int x);
```

fetches from the region of linear memory specified by the one-dimensional texture object texObj using integer texture coordinate x. tex1Dfetch() only works with non-normalized coordinates, so only the border and clamp addressing modes are supported. It does not perform any texture filtering. For integer types, it may optionally promote the integer to single-precision floating point.

### B.8.1.2. tex1D()

```
template<class T>
T tex1D(cudaTextureObject_t texObj, float x);
```

fetches from the CUDA array specified by the one-dimensional texture object texObj using texture coordinate x.

### B.8.1.3. tex1DLod()

```
template<class T>
T tex1DLod(cudaTextureObject_t texObj, float x, float level);
```

fetches from the CUDA array specified by the one-dimensional texture object texObj using texture coordinate x at the level-of-detail level.

### B.8.1.4. tex1DGrad()

```
template<class T>
T tex1DGrad(cudaTextureObject_t texObj, float x, float dx, float dy);
```

fetches from the CUDA array specified by the one-dimensional texture object texObj using texture coordinate x. The level-of-detail is derived from the X-gradient dx and Y-gradient dy.

### B.8.1.5. tex2D()

```
template<class T>
T tex2D(cudaTextureObject_t texObj, float x, float y);
```

fetches from the CUDA array or the region of linear memory specified by the two-dimensional texture object texObj using texture coordinate (x, y).

### B.8.1.6. tex2DLod()

```
template<class T>
T tex2DLod(cudaTextureObject_t texObj, float x, float y, float level);
```

fetches from the CUDA array or the region of linear memory specified by the two-dimensional texture object texObj using texture coordinate (x, y) at level-of-detail level.

### B.8.1.7. tex2DGrad()

```
template<class T>
T tex2DGrad(cudaTextureObject_t texObj, float x, float y, float dx, float dy);
```

fetches from the CUDA array specified by the two-dimensional texture object texObj using texture coordinate (x, y). The level-of-detail is derived from the dx and dy gradients.

### B.8.1.8. tex3D()

```
template<class T>
T tex3D(cudaTextureObject_t texObj, float x, float y, float z);
```

fetches from the CUDA array specified by the three-dimensional texture object texObj using texture coordinate (x, y, z).

### B.8.1.9. tex3DLod()

```
template<class T>
T tex3DLod(cudaTextureObject_t texObj, float x, float y, float z, float level);
```

fetches from the CUDA array or the region of linear memory specified by the three-dimensional texture object texObj using texture coordinate (x, y, z) at level-of-detail level.

### B.8.1.10. tex3DGrad()

```
template<class T>
T tex3DGrad(cudaTextureObject_t texObj, float x, float y, float z,
        float4 dx, float4 dy);
```

fetches from the CUDA array specified by the three-dimensional texture object texObj using texture coordinate (x,y,z) at a level-of-detail derived from the X and Y gradients dx and dy.

### B.8.1.11. tex1DLayered()

```
template<class T>
T tex1DLayered(cudaTextureObject_t texObj, float x, int layer);
```

fetches from the CUDA array specified by the one-dimensional texture object texObj using texture coordinate x and index layer, as described in Layered Textures.

### B.8.1.12. tex1DLayeredLod()

```
template<class T>
T tex1DLayeredLod(cudaTextureObject_t texObj, float x, int layer, float level);
```

fetches from the CUDA array specified by the one-dimensional layered texture at layer using texture coordinate x and level-of-detail level.

### B.8.1.13. tex1DLayeredGrad()

```
template<class T>
T tex1DLayeredGrad(cudaTextureObject_t texObj, float x, int layer,
        float dx, float dy);
```

fetches from the CUDA array specified by the one-dimensional layered texture at layer using texture coordinate x and a level-of-detail derived from the dx and dy gradients.

### B.8.1.14. tex2DLayered()

```
template<class T>
T tex2DLayered(cudaTextureObject_t texObj,
        float x, float y, int layer);
```

fetches from the CUDA array specified by the two-dimensional texture object texObj using texture coordinate (x,y) and index layer, as described in Layered Textures.

### B.8.1.15. tex2DLayeredLod()

```
template<class T>
T tex2DLayeredLod(cudaTextureObject_t texObj, float x, float y, int layer,
        float level);
```

fetches from the CUDA array specified by the two-dimensional layered texture at layer using texture coordinate (x,y).

### B.8.1.16. tex2DLayeredGrad()

```
template<class T>
T tex2DLayeredGrad(cudaTextureObject_t texObj, float x, float y, int layer,
float2 dx, float2 dy);
```

fetches from the CUDA array specified by the two-dimensional layered texture at layer **layer** using texture coordinate **(x,y)** and a level-of-detail derived from the **dx** and **dy** X and Y gradients.

### B.8.1.17. texCubemap()

```
template<class T>
T texCubemap(cudaTextureObject_t texObj, float x, float y, float z);
```

fetches the CUDA array specified by the three-dimensional texture object **texObj** using texture coordinate **(x,y,z)**, as described in Cubemap Textures.

### B.8.1.18. texCubemapLod()

```
template<class T>
T texCubemapLod(cudaTextureObject_t texObj, float x, float y, float z,
float level);
```

fetches from the CUDA array specified by the three-dimensional texture object **texObj** using texture coordinate **(x,y,z)** as described in Cubemap Textures. The level-of-detail used is given by **level**.

### B.8.1.19. texCubemapLayered()

```
template<class T>
T texCubemapLayered(cudaTextureObject_t texObj,
float x, float y, float z, int layer);
```

fetches from the CUDA array specified by the cubemap layered texture object **texObj** using texture coordinates **(x,y,z)**, and index **layer**, as described in Cubemap Layered Textures.

### B.8.1.20. texCubemapLayeredLod()

```
template<class T>
T texCubemapLayeredLod(cudaTextureObject_t texObj, float x, float y, float z,
int layer, float level);
```

fetches from the CUDA array specified by the cubemap layered texture object **texObj** using texture coordinate **(x,y,z)** and index **layer**, as described in Cubemap Layered Textures, at level-of-detail level **level**.

### B.8.1.21. tex2Dgather()

```
template<class T>
T tex2Dgather(cudaTextureObject_t texObj,
float x, float y, int comp = 0);
```
