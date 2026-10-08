![](bbox=[0.095, 0.103, 0.683, 0.381])

FIGURE 9-5

If you use two different streams, for halo computation and communication and the other for the computation of the inner region, Step 1 can be overlapped with Step 2. If the computation time required for the internal calculations is longer than the time required for the halo operations, you can realize linear speedup using multiple GPUs by hiding the performance impact of halo communication.

The pseudo code for a stencil computation with two GPUs is as follows:

```
for (int istep = 0; istep < nsteps; istep++) {
  // calculate halo in stream_halo
  for (int i = 0; i < 2; i++) {
    cudaDevice(i);
    2dfd_kernel<<<..., stream_halo[i]>>>(...);
  }
```

```
// exchange halo on stream halo
cudaMemcpyAsync(..., cudaMemcpyDeviceToDevice, stream_halo[0]);
cudaMemcpyAsync(..., cudaMemcpyDeviceToDevice, stream_halo[1]);
```

```
// calculate the internal region in stream_internal
for (int i = 0; i < 2; i++) {
  cudaDevice(i);
  2dfd_kernel<<<..., stream_internal[i]>>>(...);
}
```

```
// synchronize before next iteration
for(int i = 0; i < 2; i++) {
  cudaDevice(i);
  cudaDevicesSynchronize();
}
```