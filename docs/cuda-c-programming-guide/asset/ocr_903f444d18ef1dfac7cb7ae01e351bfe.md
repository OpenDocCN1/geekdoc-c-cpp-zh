# 3.2.11.1.3. 16-Bit Floating-Point Textures

The 16-bit floating-point or half format supported by CUDA arrays is the same as the IEEE 754-2008 binary2 format.

CUDA C++ does not support a matching data type, but provides intrinsic functions to convert to and from the 32-bit floating-point format via the `unsigned short` type: `__float2half_rn(float)` and `__half2float(unsigned short)`. These functions are only supported in device code. Equivalent functions for the host code can be found in the OpenEXR library, for example.

16-bit floating-point components are promoted to 32 bit float during texture fetching before any filtering is performed.

A channel description for the 16-bit floating-point format can be created by calling one of the `cudaCreateChannelDescHalf()` functions.

# 3.2.11.1.4. Layered Textures

A one-dimensional or two-dimensional layered texture (also known as `texture array` in Direct3D and `array texture` in OpenGL) is a texture made up of a sequence of layers, all of which are regular textures of same dimensionality, size, and data type.

A one-dimensional layered texture is addressed using an integer index and a floating-point texture coordinate; the index denotes a layer within the sequence and the coordinate addresses a texel within that layer. A two-dimensional layered texture is addressed using an integer index and two floating-point texture coordinates; the index denotes a layer within the sequence and the coordinates address a texel within that layer.

A layered texture can only be a CUDA array by calling `cudaMalloc3DArray()` with the `cudaArrayLayered` flag (and a height of zero for one-dimensional layered texture).

Layered textures are fetched using the device functions described in tex1DLayered(), tex1DLayered(), tex2DLayered(), tex2DLayered(). Texture filtering (see Texture Fetching) is done only within a layer, not across layers.

Layered textures are only supported on devices of compute capability 2.0 and higher.

# 3.2.11.1.5. Cubemap Textures

A `cubemap` texture is a special type of two-dimensional layered texture that has six layers representing the faces of a cube:

+   - The width of a layer is equal to its height.

+   - The cubemap is addressed using three texture coordinates x, y, and z that are interpreted as a direction vector emanating from the center of the cube and pointing to one face of the cube and a texel within the layer corresponding to that face. More specifically, the face is selected by the coordinate with largest magnitude m and the corresponding layer is addressed using coordinates (s/m+1)/2 and (t/m+1)/2 where s and t are defined in Table 2.