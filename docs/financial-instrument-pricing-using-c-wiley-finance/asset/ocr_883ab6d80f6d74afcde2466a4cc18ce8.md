We tested the options on square matrices of size 500, 1000 and 2000 (values are in seconds):

```
Elapsed time, Raw creation: 0.0110011
Elapsed time, Raw sequential multiply: 0.629063
Elapsed time, Raw parallel multiply PPL: 0.487049
Elapsed time, Raw parallel multiply OpenMP: 0.79708
Elapsed time, Nested creation: 0.0030003
Elapsed time, Nested sequential multiplication: 0.390039
Elapsed time, Nested parallel multiplication PPL: 0.876088
Elapsed time, Nested parallel multiplication OpenMP: 0.648065
Elapsed time, Boost creation: 0.0010001
Elapsed time, Boost sequential multiplication: 0.20302
Elapsed time, Boost parallel multiplication PPL: 1.43914
Elapsed time, Boost parallel multiplication OMP: 0.546055
Elapsed time, Duffy creation: 0.0040004
Elapsed time, Duffy sequential multiplication: 2.11721
Elapsed time, Duffy parallel multiplication OMP: 1.89219
Elapsed time, Raw creation: 0.0360036
Elapsed time, Raw sequential multiply: 15.4175
Elapsed time, Raw parallel multiply PPL: 4.64546
Elapsed time, Raw parallel multiply OpenMP: 4.88649
Elapsed time, Nested creation: 0.0070007
Elapsed time, Nested sequential multiplication: 18.1538
Elapsed time, Nested parallel multiplication PPL: 5.58186
Elapsed time, Nested parallel multiplication OpenMP: 5.45755
Elapsed time, Boost creation: 0
Elapsed time, Boost sequential multiplication: 13.0693
Elapsed time, Boost parallel multiplication PPL: 12.5833
Elapsed time, Boost parallel multiplication OMP: 5.09251
Elapsed time, Duffy creation: 0.0210021
Elapsed time, Duffy sequential multiplication: 34.8985
Elapsed time, Duffy parallel multiplication PPL: 0
Elapsed time, Duffy parallel multiplication OMP: 21.8812
Elapsed time, Raw creation: 0.169017
Elapsed time, Raw sequential multiply: 96.8327
Elapsed time, Raw parallel multiply PPL: 47.2557
Elapsed time, Raw parallel multiply OpenMP: 43.8634
Elapsed time, Nested creation: 0.0890089
Elapsed time, Nested sequential multiplication: 107.685
Elapsed time, Nested parallel multiplication PPL: 57.9658
Elapsed time, Nested parallel multiplication OpenMP: 44.6464
Elapsed time, Boost creation: 0
Elapsed time, Boost sequential multiplication: 143.671
Elapsed time, Boost parallel multiplication PPL: 106.551
Elapsed time, Boost parallel multiplication OMP: 46.0605
Elapsed time, Duffy creation: 0.0900009
Elapsed time, Duffy sequential multiplication: 221.928
Elapsed time, Duffy parallel multiplication OMP: 156.694
```

We run this code on a 2-core processor with hyperthreading. We can compare and contrast the different outputs. We see in particular that the complexity of the class structure in