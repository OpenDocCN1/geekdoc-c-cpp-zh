```
} } }
```

Here we only tested with random numbers from [-10, 10) for the real and the imaginary parts; whether this is sufficient to reach good confidence in the correctness is left open. In large projects it definitely pays off to build a reusable test framework. The pattern of nested loops containing random value generation and a test function in the innermost loop is applicable in many situations. It could be encapsulated in a class which might be variadic to handle properties involving different numbers of variables. The generation of a random value could also be provided by a special constructor (e.g., marked by a tag), or a sequence could be generated up front. Different approaches are imaginable. The loop pattern in this section was chosen for the sake of simplicity.

To see that the distributivity doesn't hold precisely, we can decrease `eps` to a very small value or even to 0. Then, we see an (abbreviated) error message like:

Click here to view code image

```
Test detected that (-6.21,7.09) * ((2.52,-3.58) +
(-4.51,-3.91))
!= (-6.21,7.09) * (2.52,-3.58) + (-6.21,7.09) *
(-4.51,3.91)
terminate called after throwing 'distributivity_violated'
```

Now we go into the details of random number generation.

# ## 4.2.2.3 Engines

The library `<random>` contains two kinds of functional objects: generators and distributions. The former generate sequences of unsigned integers (the precise type is provided by each class's type aliases). Every value should have approximately the same probability. The distribution classes map these numbers to values whose probability corresponds to the parameterized distribution.

Unless we have special needs, we can just use the `default_random_engine`. Its exact definition is implementation-dependent but we can trust the standard library developers having chosen an