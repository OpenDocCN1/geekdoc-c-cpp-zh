# LISTING 4-5 (continued)

```
cudaMalloc((innerStruct**)&d_A, nBytes);
cudaMalloc((innerStruct**)&d_C, nBytes);

// copy data from host to device
cudaMemcpy(d_A, h_A, nBytes, cudaMemcpyHostToDevice);

// set offset for summary
int blocksize = 128;
if (argc<1) blocksize = atoi(argv[1]);

// execution configuration
dim3 block(blocksize);
dim3 grid((nElem+block.x-1)/block.x);

// kernel 1: warmup
double start = seconds();
warmup << grid, block >>> (d_A, d_C, nElem);
cudaSynchronize();
double iElaps = seconds() - iStart;
printf("%d, %d, elapsed %f sec\n", grid.x, block.x, iElaps);
cudaMemcpy(gpuRef, d_C, nBytes, cudaMemcpyDeviceToHost);
checkInnerStruct(hostRef, gpuRef, nElem);

// kernel 2: testInnerStruct
iStart = seconds();
testInnerStruct << grid, block >>> (d_A, d_C, nElem);
cudaSynchronize();
iElaps = seconds() - iStart;
printf("%d, %d, elapsed %f sec\n", grid.x, block.x, iElaps);
cudaMemcpy(gpuRef, d_C, nBytes, cudaMemcpyDeviceToHost);
checkInnerStruct(hostRef, gpuRef, nElem);

// free memories both host and device
cudaFree(d_A);
cudaFree(d_C);
free(h_A);
free(hostRef);
free(gpuRef);

// reset device
cudaDeviceReset();
return EXIT_SUCCESS;
```

Compile the example with the following command, and run.

```
$ nvcc -O3 -arch=sm_20 simpleMathAo.cu -o simpleMathAo
./simpleMathAo
```

A sample output from a Fermi M2070 is included.

```
innerStruct << 8192, 128 >>> 0.0000286 sec
```