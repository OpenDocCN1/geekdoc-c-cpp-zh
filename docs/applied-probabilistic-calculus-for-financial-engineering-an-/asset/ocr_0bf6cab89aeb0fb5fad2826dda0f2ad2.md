```
[4,] 1.0000000 1.0000000
[5,] -1.6667868 2.8245124
[6,] 1.0000001 1.0000001
[7,] 1.0000001 1.0000002
[8,] 1.0000000 1.0000001
[9,] 1.0000000 1.0000000
[10,] 1.0000000 1.0000000
[11,] 1.0000000 1.0000000
[12,] 1.0000000 1.0000000
[13,] 1.0000000 1.0000000
[14,] 1.0000000 1.0000001
[15,] 1.0000000 1.0000000
[16,] 1.0000000 1.0000001
[17,] 1.0000000 1.0000001
[18,] 0.9999999 0.9999999
[19,] 1.0000000 1.0000000
[20,] -1.6708498 2.9124751

$member$storepop
list()
attr(, "class")
[1] "DEoptim"
> ## increase the population size
> DEoptim(Rosenbrock, lower, upper, DEoptim.control (NP =
> 100))
Iteration: 1 bestvalit: 0.831267 bestmemit: 0.993395 1.078004
Iteration: 2 bestvalit: 0.831267 bestmemit: 0.993395 1.078004
Iteration: 3 bestvalit: 0.136693 bestmemit: 1.238842 1.506507
Iteration: 4 bestvalit: 0.136693 bestmemit: 1.238842 1.506507
Iteration: 5 bestvalit: 0.136693 bestmemit: 1.238842 1.506507
------------------------------------------------------------
------------------------------------------------------------
Iteration: 198 bestvalit: 0.000000 bestmemit: 1.000000 1.000000
Iteration: 199 bestvalit: 0.000000 bestmemit: 1.000000 1.000000
Iteration: 200 bestvalit: 0.000000 bestmemit: 1.000000 1.000000
$optim
$optim$bestmem
par1 par2
1 1
$optim$bestval
[1] 6.981784e-23
$optim$nfeval
[1] 402
```