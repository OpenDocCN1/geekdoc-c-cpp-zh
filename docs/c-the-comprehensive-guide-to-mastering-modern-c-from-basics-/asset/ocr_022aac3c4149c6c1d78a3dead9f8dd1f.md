| Container | Description |
| --- | --- |
| gslice | Selected range of a valarray |
| slice_array | Helper class for selecting ranges of a valarray |
| gslice_array | Helper class for selecting ranges of a valarray |
| mask_array | Helper class for masking parts of a valarray |
| indirect_array | Helper class for a reordered view of a valarray |

**Table 24.14** Profile: Nonstandard “valarray” container.

There is nothing against having your own data type, except that optimizations might not apply. It may well be that you can or use a special data type for specific hardware with a third-party library. Older GPUs, for example, only supported `float` and not `double` in their CUDA libraries, but they have since advanced. CUDA is now a widely used interface to graphics cards—more widespread than the use of valarray. When speed is more important than accuracy, a half-float (16-bit floating point) might be useful. Since C++23, there has been an optional built-in data type called `float16_t` (see Chapter 4, Section 4.4.4). Or you can use other libraries. You will find it under names like `float16`, `half`, `HalfFloat`, or `__fp16` and similar. CUDA now supports it, and it is used, for example, for surface textures. CUDA and