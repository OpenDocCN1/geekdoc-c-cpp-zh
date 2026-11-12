After the allocations and data creation, we can begin the computations. We start our timer, copy our inputs to the GPU, execute the dot product kernel, and copy the partial results back to the host.

```
```c
HANDLE_ERROR ( cudaEventRecord( start, 0 ) );

// copy the arrays 'a' and 'b' to the GPU
HANDLE_ERROR ( cudaMemcpy( dev_a, a, size*sizeof( float ),
                           cudaMemcpyHostToDevice ) );
HANDLE_ERROR ( cudaMemcpy( dev_b, b, size*sizeof( float ),
                           cudaMemcpyHostToDevice ) );

dot<<<blocksPerGrid,threadsPerBlock>>> ( size, dev_a, dev_b,
                                         dev_partial_c );

// copy the array 'c' back from the GPU to the CPU
HANDLE_ERROR ( cudaMemcpy( partial_c, dev_partial_c,
                           blocksPerGrid*sizeof( float ),
                           cudaMemcpyDeviceToHost ) );
```
```

Now we need to finish up our computations on the CPU as we did in Chapter 5. Before doing this, we'll stop our event timer because it only measures work that's being performed on the GPU:

```
```c
HANDLE_ERROR ( cudaEventRecord( stop, 0 ) );
HANDLE_ERROR ( cudaEventSynchronize( stop ) );
HANDLE_ERROR ( cudaEventElapsedTime( &elapsedTime,
                                     start, stop ) );
```
```

Finally, we sum our partial results and free our input and output buffers.

```
```c
// finish up on the CPU side
c = 0;
for (int i=0; i<blocksPerGrid; i++) {
    c += partial_c[i];
}
```
```