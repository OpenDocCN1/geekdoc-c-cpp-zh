298
NUMERICAL OPTIMIZATION

in conjunction with the FM2 generator from Section 4.4 to create the three seeds that are
needed to initialize the WH generator.

the ranGen object in Listing 8.9 is used to access the ranUnit class method and thereby
produce two random uniforms from [0, 1] that are returned in the pointer pu.
two values are translated into a subinterval of [low, up] using the functions
min and max that become available by inclusion of the algorithm header as in 7.2.4.

The ordinary section method is applied to the random search intervals bounded
by low = a + (b - a)*min(po, pu[1]) and up = a + (b - a)*max(po, pu[1])
min(po, pu[0]) and max(po, pu[1]), the smaller and larger of pu and
pu[1]. This process is repeated with number nSearch times with a
check made on each iteration to see if the corresponding subinterval has a value
that improved the optimization to the minimizer.

the ranGolden method for class opt is implemented with a driver program that takes
t values of itMax, nSearch, seed and delta, in that order, as command line arguments.
The resulting executable opt was used to produce the results.

```
$ .opt 38 4 123 .0000001
nThe approximate minimizer is 0.619058
$.opt 38 5 123 .0000001
The approximate minimizer is 0.937337
```

The number of random search intervals is one the "tuning" parameter for the algorithm.
In general, the right choice for this quantity will depend on the complexity of the function
and, of course, for the generator's seed. In this instance it turns out that there are
no further improvement to six decimals by choosing nSearch to R with the optimize
function. It is also quite easy to implement the same type of random search in R with the
function that accomplishes this in the next listing.

Listing 8.10 ranGolden.r

```
#ranGolden.r
ranGolden <- function(f, a, b, nSearch, seed){
setseed(seed)
bounds <- matrix(run(2*nSearch), 2, nSearch)
minVec <- apply(bounds, MARGIN = 2,
FUN <- function(v){temp = a + (b - a)*sort(v)
optimize(f, lower = temp[1], upper = temp[2])[[2]]
location <- order(minVec)
temp = a + (b - a)*sort(bounds[1, location],
bounds[2, location])
optimize(f, lower = temp[1], upper = temp[2])
}
```

The ranGolden function has the same basic arguments as its C++ analog; the objective
function f, the lower and upper limits of the search interval a and b, the number of random\searches to be performed and the value of the initial seed for the random number generator.
The first line of the function's body sets the seed for the local environment to
t supplied value of random is generated using the R set.seed function. Next, an array named
of this array will be used to construct the random subintervals of [0, 1] which to optimize
will be applied. The function manages the search. Its input argument is the bounds
array. Sorting each pair of random uniforms and rescaling them to fall in the search interval
ween a and b. The optimize function is applied to this subinterval and only the second
component from its output is retained. The result is that the output from apply is a