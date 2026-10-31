```
$member$storepop
list()
attr(", "class")
[1] "DEoptim"
>
> Genrose <- function(x) {
+ ## One generalization of the Rosenbrock banana valley function
+ (n parameters)
+ n <- length(x)
+ ## make it take some time ...
+ Sys.sleep(.001)
+ 1.0 + sum (100 * (x[n-1]^2 - x[-1])^2 + (x[-1] - 1)^2)
+ }
>
> # get some run-time on simple problems
> maxIt <- 250
> n <- 5
> oneCore <- system.time (DEoptim(fn=Genrose, lower=rep(-25, n),
+ upper=rep(25, n),
+ control=list(NP=10*n, itermax=maxIt)))
Iteration: 1 bestvalit: 67180.992768 bestmemit: 0.787009
-4.017866 4.091383 -2.065631 -7.987533
Iteration: 2 bestvalit: 67180.992768 bestmemit: 0.787009
-4.017866 4.091383 -2.065631 -7.987533
Iteration: 3 bestvalit: 67180.992768 bestmemit: 0.787009
-4.017866 4.091383 -2.065631 -7.987533
Iteration: 4 bestvalit: 67180.992768 bestmemit: 0.787009
-4.017866 4.091383 -2.065631 -7.987533
Iteration: 5 bestvalit: 42308.544031 bestmemit: 0.787009
-4.017866 0.493543 -2.065631 -7.987533
------------------------------------------------
Iteration: 248 bestvalit: 1.079131 bestmemit: -1.005728
0.991545 0.993995 1.004214 1.004883
Iteration: 249 bestvalit: 1.079131 bestmemit: -1.005728
0.991545 0.993995 1.004214 1.004883
Iteration: 250 bestvalit: 1.079131 bestmemit: -1.005728
0.991545 0.993995 1.004214 1.004883
> withParallel <- system.time (DEoptim(fn=Genrose, lower=rep
(-25, n), upper=rep(25, n),
+ control=list(NP=10*n, itermax=maxIt, parallelType=1)))
Iteration: 1 bestvalit: 1036700.619060 bestmemit: 8.705266
3.108165 -7.886303 -3.630207 -7.869868
```