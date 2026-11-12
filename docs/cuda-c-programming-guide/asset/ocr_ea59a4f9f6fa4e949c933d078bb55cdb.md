# B.8.2.3. tex1DLod()

```
template<class DataType, enum
cudaTextureReadMode readMode>
Type tex1DLod(texture<DataType, cudaTextureType1D, readMode> texRef, float x,
float level);
```

fetches from the CUDA array bound to the one-dimensional texture reference texRef using texture coordinate x. The level-of-detail is given by level. Type is the same as DataType except when readMode is cudaReadModeNormalizedFloat (see Texture Reference API), in which case Type is the corresponding floating-point type.

# B.8.2.4. tex1DGrad()

```
template<class DataType, enum
cudaTextureReadMode readMode>
Type tex1DGrad(texture<DataType, cudaTextureType1D, readMode> texRef, float x,
float dx, float dy);
```

fetches from the CUDA array bound to the one-dimensional texture reference texRef using texture coordinate x. The level-of-detail is derived from the dx and dy X- and Y-gradients. Type is the same as DataType except when readMode is cudaReadModeNormalizedFloat (see Texture Reference API), in which case Type is the corresponding floating-point type.

# B.8.2.5. tex2D()

```
template<class DataType, enum cudaTextureReadMode readMode>
Type tex2D(texture<DataType, cudaTextureType2D, readMode> texRef,
float x, float y);
```

fetches from the CUDA array or the region of linear memory bound to the two-dimensional texture reference texRef using texture coordinates x and y. Type is equal to DataType except when readMode is equal to cudaReadModeNormalizedFloat (see Texture Reference API), in which case Type is equal to the matching floating-point type.

# B.8.2.6. tex2DLod()

```
template<class DataType, enum
cudaTextureReadMode readMode>
Type tex2DLod(texture<DataType, cudaTextureType2D, readMode> texRef,
float x, float y, float level);
```

fetches from the CUDA array bound to the two-dimensional texture reference texRef using texture coordinate (x,y). The level-of-detail is given by level. Type is the same as DataType except when readMode is cudaReadModeNormalizedFloat (see Texture Reference API), in which case Type is the corresponding floating-point type.

# B.8.2.7. tex2DGrad()

```
template<class DataType, enum
cudaTextureReadMode readMode>
Type tex2DGrad(texture<DataType, cudaTextureType2D, readMode> texRef,
float x, float y, float2 dx, float2 dy);
```