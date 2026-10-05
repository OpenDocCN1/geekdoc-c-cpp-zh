# CUDA and C++

CUDA was born from the C++ family, and naturally, it integrates seamlessly with C++ applications. This synergy is particularly advantageous for performance-critical software that already leverages C++ for its efficiency and control.

Using CUDA in C++ involves a mix of conventional C++ code and CUDA kernels. CUDA C++ files typically have a .cu extension and are compiled with the nvcc compiler, which understands both CUDA and standard C++ code. Here is a basic example illustrating the integration of a CUDA kernel within a C++ program:

```
#include#include __global_ void *d_out, float *d_in) int idx =
threadIdx.x; f = d_in[idx]; f = f * f; } int main() { int ARRAY_SIZE = 64;
int ARRAY_BYTES = ARRAY_SIZE * Generate input array on the host
h_in[ARRAY_SIZE]; i = 0; i < ARRAY_SIZE; i++) {
h_out[ARRAY_SIZE]; Declare GPU memory pointers *d_in; *d_out;
Allocate GPU memory &d_in, ARRAY_BYTES); &d_out,
ARRAY_BYTES); Transfer the array to the GPU h_in, ARRAY_BYTES,
cudaMempyHostToDevice); Launch the kernel ARRAY_SIZE>>>
(d_out, d_in); Copy back the result array to the CPU d_out,
ARRAY_BYTES, cudaMempyDeviceToHost); Print the results = i = 0; i <
ARRAY_SIZE; i++) { << h_out[i] << std::endl; Free GPU memory 0; }
```