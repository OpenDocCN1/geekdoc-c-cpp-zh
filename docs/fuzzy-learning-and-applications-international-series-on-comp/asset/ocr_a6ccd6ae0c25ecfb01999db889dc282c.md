| t' (s) | e (RMNSE %) | Runs | t(e) (s) |
|---|---|---|---|
| 0.5 | 3.41779 | 88 | 0.41 |
| 1 | 3.39518 | 128 | 0.59 |
| 2 | 3.31133 | 318 | 1.50 |
| 4 | 3.23319 | 528 | 3.02 |

Table 1.14 Results obtained when all PEs are used and no exchange of data among slaves is permitted

phase converges and no significant improvements are reachable in a reasonable time. Too long simulations with a number of PEs with a low P_{p,c} would imply very high artificial speedups.

For these two reasons the simulations using one p233 were chosen to last 300s, 150 and 75s.

Figure 1.23 clearly states that the implementation of GEFREX gains significantly in performance when many PEs are used. Given that the network is always utilized less than 10% of its maximum possibility the results are surprising: PARGEFREX is particularly suited for commodity supercomputers rather than very expensive servers with few processors.

Figure 1.23 confirms our discussion regarding too long simulations. If one p233 is used and the simulations last for 300s the speedup is particularly high: almost 450! This phenomenon is due to the fact that after 100-200s all the simulations converge and do not succeed in improving significantly. If we evaluated the average error when the simulation time was greater we would have a huge speedup, because the error would be almost identical to that found in 300s. Simulations using a p233 that last for 75s and 150s are more suited to evaluating the speedup.

The reader can see that the speedup is always greater than one. This fact implies a clear concept: the use of several PEs rather than only one permits the finding, on average, of very low learning errors. It is very improbable to find the same error with only one PE even if many very long simulations are launched. In this sense we can say that PARGEFREX is more effective than GEFREX.

To understand how important inter-slave communication is, PARGEFREX was used avoiding any exchange of individuals. Table 1.14 shows the results obtained when all PEs are used and the CT criterion was chosen with the simulation times fixed respectively to 0.5, 1.2 and 4 seconds. The last column reports the time that would be needed in the case of a migration time of 0.1s. There is a clear advantage permitting migration. With the fastest simulation the advantage is less evident in comparison to other cases, but it needs to be underlined that in this case the simulation time is almost all constituted by the neuro-phase and the genetic phase, where migration is allowed, is very short.