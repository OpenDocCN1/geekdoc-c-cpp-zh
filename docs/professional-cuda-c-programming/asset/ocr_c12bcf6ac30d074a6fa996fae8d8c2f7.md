than a PRNG. You can think of these direction vectors as a starting direction to begin exploring the n-dimensional space which random bits are extracted. Here, they are in a sense that they are a piece of human-provided initial randomness, even though they are called by a different name. In the cuRAND host API, only the number of dimensions to use for QRNGs can be set using curandSetQuasiRandomGeneratorDimensions:

```
curandGenerator_t rand_state;
curandCreateGenerator(&rand_state, curRAND_RNG_QUASI_SOBOL32);
candSetQuasiRandomGeneratorDimensions(rand_state, 2);
```

However, the API allows the direction vectors to be explicitly set:

```
_global void kernel(curandDirectionVectors32_t *direction_vector, ... )
{\n  curandStatesSobol32_t rand_state;
  curand_init(*direction_vector, 0, &rand_state);
}
```

```
curandDirectionVectors32_t *h_vectors;
curandGetDirectionVectors32(d_vectors, h_vectors, sizeof(curandDirectionVectors32_t),
cudaMemcpy(d_vectors, h_vectors, sizeof(curandDirectionVectors32_t),
kernel<<<blocks, threads>>>(d_vectors, ...);
```

Finally, the offset in cuRAND is the offset in a sequence of random numbers at to start. Each seed produces a different sequence of random numbers. The offset allows you to jump to the i-th random value in sequence. In the host API, this is set using the function curandSetGeneratorOffset:

```
curandGenerator_t rand_state;
curandCreateGenerator(&rand_state, curRAND_RNG_PSEUDO_DEFAULT);
curandSetGeneratorOffset(rand_state, offset, GULL);
```

In the cuRAND API, the offset is set as a parameter to the curand_init function (similar to seeds):

```
_device void curand_init(unsigned long long seed, unsigned long long subsequence, unsigned long long offset, curandStateXOROW_t *state);
```

# Comparing the Host and Device APIs

Deciding whether to use the host or device cuRAND API is an application-specific decision. Both APIs provide similar capabilities in terms of functionality: the same RNGs, the same distributions, and the same configuration of different parameters. However, the methods used to access capability are very different. This section provides guidelines on the selection process based on your application requirements.

If your only goal is efficient, high-quality random number generation for what is otherwise an entirely host application, the host API is the best choice. It has been hand-tuned by CUDA experts to produce optimal performance for this use case and is far more usable than writing