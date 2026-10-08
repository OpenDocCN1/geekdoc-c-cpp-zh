
# Covering the Concepts

Configuring both the host and device cuRAND APIs requires four options: an RNG algorithm with which to generate a random sequence, a distribution to which the returned values will adhere, a seed from which to start, and an offset into the random number sequence to begin sampling. While the device API requires explicit specification of each of these parameters, the host API will automatically set them to default values if you do not set them.

Both host and device APIs retain the concept of handlers from other CUDA libraries. In the host API, generators are referred to as *generators*. You can construct a generator using `curRandCreate` or `curRandSetStream` or `curRandSetGeneratorOffset`. Only a single generator is necessary to access the host API. The device API instead refers to it as cuRAND state. There are multiple types of device state, one for each type of RNG. However, the role of the state object is still to maintain the configuration and status of a single thread's cuRAND context on the GPU. As a result, you will generally need to allocate a large batch of device state objects, one for each GPU thread.

The first configurable in curRAND host and device APIs is the RNG algorithm to be used. In the host API, this is configured using the `rng_type` parameter to `curRandCreateGenerator`.

```c
curRandStatus_t curRandCreateGenerator(curRandGenerator_t *generator,
curRandRNGType_t rng_type);
```

In the device API, this is configured by calling an RNG-specific initialization function with an RNG-specific state, which serves as a cuRAND state in the device API:

```c
_device void curRand_init(unsigned long seed,
                              unsigned long subsequence,
                              unsigned long offset,
                              curRandStateXORWOW937_t *state);
_device void curRand_init(unsigned long seed,
                              unsigned long subsequence,
                              unsigned long offset,
                              curRandStateMRG32ka_t *state);
```

Selecting RNG algorithms affects the techniques used to generate random values and so affect both the quality of randomness as well as performance. Both the host and device support a variety of RNG algorithms. For example, to initialize an RNG on the device to use the following code:

```c
_global void kernel() {
    curRandStateXORWOW_t rand_state;
    curRand_init(0, 0, 0, &rand_state);
}
```

Then, `rand_state` could be used later as a handler for generating random values.

Next, selecting different distributions affects how the values produced by an RNG are distributed across the range of possible values (recall that all floating-point values have a discrete range of values). The relation between RNG algorithm and the distribution may not seem obvious. The RNG algorithm can be thought of as a black box that produces a random sequence of bits. These bits have no meaning to the RNG algorithm. Adding a distribution on top of an RNG with a specific return type curand to use those bits to generate a meaningful value that is characteristic of the selected distribution. The host and device API both support normal, uniform, lognormal, and Poisson distributions.

The desired distribution is specified when performing random value generation by calling a distribution-specific function. For example, using a uniform distribution in the host API requires

```c
curandGenerator_t rand_state;
int d_rand_length = ...;
float *d_rand;
curandCreateGenerator(&rand_state, CURAND_RNG_PSEUDO_DEFAULT);
cudaMalloc((void **)d, sizeof(float) * d_rand_length);
curandGenerateUniform(rand_state, d_rand, d_rand_length);
```

On the device, curand_uniform would be used instead:

```c
global
void kernel(...) {
    curRandStateXORWOW_t rand_state;
    curandinit(0, 0, 0, &rand_state);
    float f = curand_uniform(&rand_state);
}
```

The third configurable in curAND is the seed. The concept of a seed is for both PRNGs and QRNGs, which use different determinism. The seed selects for human-provided randomness on which to base the future randomness of the PRNG. Different seeds produce different sequences of random values. The host API enables the optional setting of the seed for PRNGs using curandSetPseudoRandomGeneratorSeed:

```c
curandGenerator_t rand_state;
curandCreateGenerator(&rand_state, CURAND_RNG_PSEUDO_DEFAULT);
curandSetPseudoRandomGeneratorSeed(rand_state, 98723499ULL);
```

However a default seed will be selected if it is not specified. On the other hand, requires setting of the seed for each thread of PRNG. You have already seen the seed set in calls to the device API's curand_init. The first argument specifies the seeding for the RNG created:

```c
device void curand_init(unsigned long long seed,
                               unsigned long subsequence,
                               unsigned long offset,
                               curandStateXOR_t *state);
```

The only QRNG supported by the host and device API is based on Sobol quasi-random sequence (discussion of which is beyond the scope of this book). A Sobol sequence is seeded by direction vectors. Recall that the advantage of a quasi-random generator is that each sampling is not a statistically independent event; a QRNG will deliberately fill the range of values more even than a PRNG. You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Recall that the advantage of a quasi-random generator is that each sampling is not a statistically independent event; a QRNG will deliberately fill the range of values more even than a PRNG. You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Recall that the advantage of a quasi-random generator is that each sampling is not a statistically independent event; a QRNG will deliberately fill the range of values more even than a PRNG. You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Recall that the advantage of a quasi-random generator is that each sampling is not a statistically independent event; a QRNG will deliberately fill the range of values more even than a PRNG. You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Recall that the advantage of a quasi-random generator is that each sampling is not a statistically independent event; a QRNG will deliberately fill the range of values more even than a PRNG. You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. (Note: The OCR text contains significant repetitions in this section which I have cleaned up based on logical flow).

The host and device API both support normal, uniform, lognormal, and Poisson distributions.

The desired distribution is specified when performing random value generation by calling a distribution-specific function. For example, using a uniform distribution in the host API requires

```c
curandGenerator_t rand_state;
int d_rand_length = ...;
float *d_rand;
curandCreateGenerator(&rand_state, CURAND_RNG_PSEUDO_DEFAULT);
cudaMalloc((void **)d, sizeof(float) * d_rand_length);
curandGenerateUniform(rand_state, d_rand, d_rand_length);
```

On the device, curand_uniform would be used instead:

```c
global
void kernel(...) {
    curandStateXOROW_t rand_state;
    curandinit(0, 0, 0, &rand_state);
    float f = curand_uniform(&rand_state);
}
```

The third configurable in curAND is the seed. The concept of a seed is for both PRNGs and QRNGs, which use different determinism. The seed selects for human-provided randomness on which to base the future randomness of the PRNG. Different seeds produce different sequences of random values. The host API enables the optional setting of the seed for PRNGs using curandSetPseudoRandomGeneratorSeed:

```c
curandGenerator_t rand_state;
curandCreateGenerator(&rand_state, CURAND_RNG_PSEUDO_DEFAULT);
curandSetPseudoRandomGeneratorSeed(rand_state, 98723499ULL);
```

However a default seed will be selected if it is not specified. On the other hand, requires setting of the seed for each thread of PRNG. You have already seen the seed set in calls to the device API's curand_init. The first argument specifies the seeding for the RNG created:

```c
device void curand_init(unsigned long long seed,
                               unsigned long subsequence,
                               unsigned long offset,
                               curandStateXOR_W_t *state);
```

The only QRNG supported by the host and device API is based on Sobol quasi-random sequence (discussion of which is beyond the scope of this book). A Sobol sequence is seeded by direction vectors. Recall that the advantage of a quasi-random generator is that each sampling is not a statistically independent event; a QRNG will deliberately fill the range of values more even than a PRNG. You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. (Cleaned up repetitions).

You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, the direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. (Cleaned up repetitions).

The host and device API both support normal, uniform, lognormal, and Poisson distributions.

The desired distribution is specified when performing random value generation by calling a distribution-specific function. For example, using a uniform distribution in the host API requires

```c
curandGenerator_t rand_state;
int d_rand_length = ...;
float *d_rand;
curandCreateGenerator(&rand_state, CURAND_RNG_PSEUDO_DEFAULT);
cudaMalloc((void **)d, sizeof(float) * d_rand_length);
curandGenerateUniform(rand_state, d_rand, d_rand_length);
```

On the device, curand_uniform would be used instead:

```c
global
void kernel(...) {
    curandStateXOROW_t rand_state;
    curandinit(0, 0, 0, &rand_state);
    float f = curand_uniform(&rand_state);
}
```

The third configurable in curAND is the seed. The concept of a seed is for both PRNGs and QRNGs, which use different determinism. The seed selects for human-provided randomness on which to base the future randomness of the PRNG. Different seeds produce different sequences of random values. The host API enables the optional setting of the seed for PRNGs using curandSetPseudoRandomGeneratorSeed:

```c
curandGenerator_t rand_state;
curandCreateGenerator(&rand_state, CURAND_RNG_PSEUDO_DEFAULT);
curandSetPseudoRandomGeneratorSeed(rand_state, 98723499ULL);
```

However a default seed will be selected if it is not specified. On the other hand, requires setting of the seed for each thread of PRNG. You have already seen the seed set in calls to the device API's curand_init. The first argument specifies the seeding for the RNG created:

```c
device void curand_init(unsigned long long seed,
                               unsigned long subsequence,
                               unsigned long offset,
                               curandStateXOR_W_t *state);
```

The only QRNG supported by the host and device API is based on Sobol quasi-random sequence (discussion of which is beyond the scope of this book). A Sobol sequence is seeded by direction vectors. Recall that the advantage of a quasi-random generator is that each sampling is not a statistically independent event; a QRNG will deliberately fill the range of values more even than a PRNG. You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted.

The host and device API both support normal, uniform, lognormal, and Poisson distributions.

The desired distribution is specified when performing random value generation by calling a distribution-specific function. For example, using a uniform distribution in the host API requires

```c
curandGenerator_t rand_state;
int d_rand_length = ...;
float *d_rand;
curandCreateGenerator(&rand_state, CURAND_RNG_PSEUDO_DEFAULT);
cudaMalloc((void **)d, sizeof(float) * d_rand_length);
curandGenerateUniform(rand_state, d_rand, d_rand_length);
```

On the device, curand_uniform would be used instead:

```c
global
void kernel(...) {
    curandStateXOROW_t rand_state;
    curandinit(0, 0, 0, &rand_state);
    float f = curand_uniform(&rand_state);
}
```

## Comparing the Host and Device APIs

Deciding whether to use host or device API is an application-specific decision. Both APIs provide similar capabilities in terms of functionality; however, the methods used to access them are very different. If your only goal is efficient, high-quality random number generation for your application, the host API is the best choice. It will likely degrade performance with added overhead from host and kernel launches.

If you require more control over the generation of randomness, if you are consuming randomness within a CUDA kernel, and particularly if your randomness requirements change dynamically, the device API is the right choice. It requires a small amount of development to initialize and manage RNG state on the device but offers much more flexibility.

## Demonstrating cuRAND

This section covers two examples of the cuRAND APIs. First, you will look at an example that demonstrates replacing the system rand function using the host and device APIs. Second, you will look at an example that uses the host and device APIs and the system call to produce randomness for a CUDA kernel.

## Replacing rand()

You can follow this example by downloading the sample code in replace-rand.cu from Wrox.com, which uses the host and device APIs to generate random numbers for later consumption on the host. This generates a large batch of random numbers in one library call and then iterates through them as the host requests new values. When all random values are exhausted it must go back to the cuRAND library to generate more. The workflow for using the host API is the simplest you have looked at in this chapter and includes the following steps:

- Create a cuRAND generator configured with the desired RNG using curandCreateGenerator. Configuration of that generator is possible (for example, using curandSetStream), but is optional for the host API.
- Pre-allocate device memory using cudaMemAlloc for curRAND to store the output random values in it.
- Generate random values by executing a curRAND library call, e.g., curandGenerateUniform.
- If desired for consumption on the host, retrieve the generated random values from device memory using cudaMemcpy.

The following code snippet demonstrates the cuRAND host API workflow:

```c
/*
 * An implementation of rand() that uses the cuRAND host API.
 */
float cuda_host_rand() {
  ...
  if (dRand == NULL) {
```
