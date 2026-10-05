# Example

Consider a CUDA kernel that accesses a 2D texture for image processing.
The example code shows how to allocate a CUDA array, bind it to a texture reference, and access it within a kernel to perform bilinear filtering.

```
// Define texture reference cudaType2D,
cudaReadModeElement<Type> texRef; __global__ void *output, int
imageWidth, int imageHeight) { x = blockIdx.x * blockDim.x + 
threadIdx.x; y = blockIdx.y * blockDim.y + threadIdx.y; (x :=
imageWidth || y >= imageHeight) u = x / v = y / Sampling from the texture
pixel = tex2D(texRef, u, v); * imageWidth + x] = pixel; } int main() {
Create and bind texture cuArray; &texRef.channelDesc, width, height); 0;
0, hostImage, size, cudaMemcpyHostToDevice); cuArray,
texRef.channelDesc); Call kernel blocks(16, 16); grid((width + blocks.x -
1) / blocks.x, (height + blocks.y - 1) / blocks.y); blocks>>>(deviceOutput,
width, height); Clean up }
```