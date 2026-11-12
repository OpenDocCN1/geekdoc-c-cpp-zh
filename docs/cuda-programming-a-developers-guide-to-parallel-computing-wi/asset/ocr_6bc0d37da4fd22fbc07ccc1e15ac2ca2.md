```
```c
// Allocate host memory
int * const host_raw_ptr_2 = (int *) malloc(size_in_bytes);
int *p2 = host_raw_ptr_2;

if ( (host_raw_ptr_2 == NULL) )
{
    printf(*"\nError allocating host memory for extraction of thrust data*":
    exit(0);
}

// Extract data from Thrust vector to normal memory block
for (int i=0; i<num_elems; i++)
{
    *p2++ = host_array[i];
}

reduce_h_mp_t = get_time();
const long int sum_host_omp = reduce_openmp(host_raw_ptr_2, num_elems);
reduce_h_mp_t = (get_time() - reduce_h_mp_t);

reduce_h_serial_t = get_time();
const long int sum_host_serial = reduce_serial(host_raw_ptr_2, num_elems);
reduce_h_serial_t = (get_time() - reduce_h_serial_t);

// Free memory
free(host_raw_ptr_2);

if ( (sum_host == sum_device) && (sum_host == sum_host_omp) )
    printf(*"\nReduction Matched*");
else
    printf(*"\n**** FAILED ****");

// Calculate time for each aspect
CUDA_CALL(cudaEventElapsedTime(&c2d_t, c2d_start, c2d_stop));
CUDA_CALL(cudaEventElapsedTime(&reduce_d_t, sort_d_start, sort_d_stop));

printf(*"\nCopy To Device : %.2fms*", c2d_t);
printf(*"\nReduce On Device : %.2fms*", reduce_d_t);
printf(*"\nTotal Device Time : %.2fms*", c2d_t + reduce_d_t);
printf(*"\nInthrust Reduce On Host: %.2fms*", reduce_h_t);
printf(*"\nSerial Reduce On Host: %.2fms*", reduce_h_serial_t);
printf(*"\nOpenMP Reduce On Host: %.2fms*", reduce_h_mp_t);

CUDA_CALL(cudaEventDestroy(c2d_start));
CUDA_CALL(cudaEventDestroy(c2d_stop));
CUDA_CALL(cudaEventDestroy(sort_d_start));
CUDA_CALL(cudaEventDestroy(sort_d_stop));
}

return 0;
```
```