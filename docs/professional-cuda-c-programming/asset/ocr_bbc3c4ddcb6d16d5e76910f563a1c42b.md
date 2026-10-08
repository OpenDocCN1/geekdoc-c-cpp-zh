# LISTING 2-4 (continued)

```
// initialize data at host side
initialData(h_A, nElem);
initialData(h_B, nElem);

memset(hostRef, 0, nBytes);
memset(gpuRef, 0, nBytes);

// allocate device global memory
float *d_A, *d_B, *d_C;
cudaMalloc((float**)&d_A, nBytes);
cudaMalloc((float**)&d_B, nBytes);
cudaMalloc((float**)&d_C, nBytes);

// transfer data from host to device
cudaMemcpy(gpuRef, d_A, h_A, nBytes, cudaMemcpyHostToDevice);
cudaMemcpy(d_B, h_B, nBytes, cudaMemcpyHostToDevice);

// invoke kernel at host side
dim block(nElem);
drid grid(nElem/block.x);
sumArraysOnGPU(grid, block) >>>(d_A, d_B, d_C);
printf("Execution configuration <<%d, %d>>\n", grid.x, block.x);

// copy kernel result back to host side
cudaMemcpy(hostRef, d_C, nBytes, cudaMemcpyDeviceToHost);

// add vector at host side for result checks
sumArraysOnHostHost(h_A, h_B, hostRef, nElem);

// check device results
checkresult(hostRef, gpuRef, nElem);

// free device global memory
cudaFree(d_A);
cudaFree(d_B);
cudaFree(d_C);

// free host memory
free(h_A);
free(h_B);
free(hostRef);
free(gpuRef);

return(0);
```

In this code, the vector size was set to 32 as follows:

```
int nElem = 32;
```