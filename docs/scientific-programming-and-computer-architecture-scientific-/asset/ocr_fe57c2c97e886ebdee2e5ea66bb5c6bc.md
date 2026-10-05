# Chapter 6. Special Topic: Networks and Message Passing

| nprocs | dim1 | dim2 | cycles/entry/itn |
|--- | --- | --- | --- |
| 4 | $10^5$ | $12 	imes 10^3$ | 8.3 |
| 20 | $10^5$ | $12 	imes 10^3$ | 7.2 |
| 100 | $10^5$ | $12 	imes 10^3$ | 7.7 |

Table 6.4: Performance of the Jacobi2D class on nprocs nodes, each a 2-core 3.33 GHz SSE2 machine (see table A.1).

```
13 jacobi.copypp
14     }
15     return clk.toc();
16 }
```

The OpenMP constructs are hidden away inside the implementation of the Jacobi2D class. There are no OpenMP constructs within the iteration loop.

The wait() on line 11 immediately follows postsendrecv() on line 12. The implementation waits for the message to be complete after initiating sends and receives. No attempt is made to overlap computation with communication because there is no need for it. Message passing takes up an insignificant amount of time in this program, and any effort to hide its cost by overlapping it with computation would be wasted. Indeed, an attempt at such an optimization may make the loop nests in the member functions update() and copy() more complicated, leading to a slightly slower program.

# Timing the Jacobi class

The three trials reported in table 6.4 take $dim1 = 10^5$ and $dim2 = 12,000$ on each MPI process. The number of MPI processes, with one process per Xeon 5680 compute node, varies from 4 to 100. The size of the matrix local to each MPI process or compute node is thus equal to $10^5 	imes 12,002$. The performance reported is the number of cycles consumed per iteration divided by the number of entries local to each MPI process.

During each iteration, four arithmetic operations (three additions and a multiplication) are performed to update each entry. Corresponding to update, two entries, one within the array a[] and one within b[] are accessed. Thus, approxi