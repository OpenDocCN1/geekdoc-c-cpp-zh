# 142 GENERATION OF PSEUDO-RANDOM NUMBERS

# 4.8 Generating random numbers in R

As described in Appendix B, the R language provides the facility for obtaining random deviates from most of the standard distributions used in statistics. Random numbers for a distribution MyDist are produced with syntax such as

```
rMyDist(n, ...)
```

with n being the desired sample size and ... indicating other arguments that might be needed for a particular distribution of interest.

The type of random number generator that is used in the rMyDist functions can be determined and set using the RNGKind. Entering RNGKind() will return two values: the generator that is used to generate uniforms and the generator that is used to generate normals. The default generator is the Mersenne Twister. There are other options, including the VH generator, which are listed in the R help page for RNGKind. The default method for generating random deviates is direct inversion. There are four other options of which is the Box-Muller method. A user-specified method can also be employed for generating either uniforms or normals.

To choose one of the other options for generating uniforms or normals, simply specify a value for one or both of the RNGKind and determine the uniform and normal generator, respectively. The ensuing code segments querying for the current generator choices and changing them to the Wichmann-Hill and Box-Muller methods.

+   * RNGKind()
[1] Mersenne-Twister "Inversion"
* RNGKind(kind = "Wichmann-Hill", normal.kind = "Box-Muller")
* RNGKind()
[1] Wichmann-Hill "Box-Muller"

Although the Mr32k3a generator from the RngStreams package discussed in Section 4.5 is not one of the options that can be chosen with RNGKind, it can be accessed through the rstream package. After loading the package with

+   * library("rstream")

the random number generator for the R session can be set as Mr32k3a via the command

```
rstream.RNG(stream("rstream.mr32k3a", seed = =))
```

with A seed of six integers. A portion of an R session illustrates that the idea shown below.

+   * library("rstream")
* rstream.RNG(new("rstream.mr32k3a", seed = c(1, 2, 3, 4, 5, 6)))
* runif(1)
[1] 0.00100948

The seed argument chosen to be the same as the one that was used in the Mr32k3a generator from RngStreams in Section 4.5. The output indicates that the Mr32k3a generator with this seed is now being used to generate uniforms in R.

In order to recreate data that has been previously produced by a random number generator we need to know the seed or seeds that were used in the generator. The function set seed is an integer variable seed that is used to set whatever seeds are required for the chosen generator method. In the example shown below seed is first set to 123. Then two sets of five random normals are generated. The second set of five is different from the first