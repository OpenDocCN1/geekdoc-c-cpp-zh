# Covering the Concepts

Configuring both the host and device cuRAND APIs requires four options: an RNG algorithm with which to generate a random sequence, a distribution to which the returned values will adhere, a seed from which to start, and an offset into the random number sequence to begin sampling. While the device API requires explicit specification of each of these parameters, the host API will automatically set them to default values if you do not set them.

Both host and device APIs retain the concept of handlers from other CUDA libraries. In the host API, generators are referred to as *generators*. You can construct a generator using `curRandCreate` or `curRandSetStream` or `curRandSetGeneratorOffset`. Only a single generator is necessary to access the host API. The device API instead refers to it as cuRAND state. There are multiple types of device state, one for each type of RNG. However, the role of the state object is still to maintain the configuration and status of a single thread's cuRAND context on the GPU. As a result, you will generally need to allocate a large batch of device state objects, one for each GPU thread.

The first configurable in curRAND host and device APIs is the RNG algorithm to be used. In the host API, this is configured using the `rng_type` parameter to `curRandCreateGenerator`.

```
curRandStatus_t curRandCreateGenerator(curRandGenerator_t *generator,
curRandRNGType_t rng_type);
```

In the device API, this is configured by calling an RNG-specific initialization function with an RNG-specific state, which serves as a cuRAND state in the device API:

```
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

```
_global void kernel() {
    curRandStateXORWOW_t rand_state;
    curRand_init(0, 0, 0, &rand_state);
}
```

Then, `rand_state` could be used later as a handler for generating random values.

Next, selecting different distributions affects how the values produced by an RNG are distributed across the range of possible values (recall that all floating-point values have a discrete