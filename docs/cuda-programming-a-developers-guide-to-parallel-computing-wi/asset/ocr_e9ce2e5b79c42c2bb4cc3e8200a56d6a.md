```
printf("%2d: %f ", i, data[i]);
}

__host__ int main(int argc, char *argv[])
{
    const int num_elem = 32;
    const size_t size_in_bytes = (num_elem * sizeof(float));

    curandGenerator_t rand_generator_device, rand_generator_host;
    const unsigned long int seed = 987654321;
    const curandRngType_t generator_type = CURAND_RNG_PSEUDO_DEFAULT;

    // Allocate memory on the device
    float * device_ptr;
    CUDA_CALL(cudaMalloc((void **)&device_ptr, size_in_bytes));

    // Allocate memory on the host for the device copy
    float * host_ptr;
    CUDA_CALL(cudaMallocHost((void **)&host_ptr, size_in_bytes));

    // Allocate memory on the host for the host version
    float * host_gen_ptr = (float *) malloc(size_in_bytes);
    if (host_gen_ptr == NULL)
    {
        printf("Failed to allocation memory on host");
        exit(0);
    }

    // Print library version number
    int version;
    CURAND_CALL(curandGetVersion(&version));
    printf("Using CuRand Version: %d and generator: CURAND_RNG_PSEUDO_DEFAULT",
           version);

    // Register the generator - note the different function calls
    CURAND_CALL(curandCreateGenerator(&rand_generator_device, generator_type));
    CURAND_CALL(curandCreateGenerator(&rand_generator_host, generator_type));

    // Set the seed for the random number generators
    CURAND_CALL(curandSetPseudoRandomGeneratorSeed(rand_generator_device, seed));
    CURAND_CALL(curandSetPseudoRandomGeneratorSeed(rand_generator_host, seed));

    // Create a set of random numbers on the device and host
    CURAND_CALL(curandGenerateUniform(rand_generator_device, device_ptr, num_elem));
    CURAND_CALL(curandGenerateUniform(rand_generator_host, host_gen_ptr, num_elem));

    // Copy the set of device generated data to the host
    CUDA_CALL(cudaMemcpy(host_ptr, device_ptr, size_in_bytes, cudaMemcpyDeviceToHost));
```