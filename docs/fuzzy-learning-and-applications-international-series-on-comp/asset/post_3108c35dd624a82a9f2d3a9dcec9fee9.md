
![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_57_0.png)

Figure 1.23 (+) Simulation time ≈ 300s/P_{p,c} (×) ≈ 150s/P_{p,c} (⊕) ≈ 75s/P_{p,c} (∇) Linear speedup

- The first one is related to the total power of our machine and the high S_{p,c} values obtained. The shorter simulation using only one p233 must correspond to a significant point in the curve shown in Figure 1.22. Table 1.13 shows that with one p233 and 75s of learning time an error of about 3.41% is reached on average. This value corresponds (see Figure 1.22) to about 0.2-0.4s using all PEs. This value is at the limit. In fact, we remember that, as explained in describing Figures 1.19 and 1.20, when learning time is less than about 0.3-0.4s, the learning process is only in the neuro phase where the initial population is generated and no communication among PEs is allowed. So, to evaluate well the speed up achievable by the proposed implementation of PARGEFREX, simulations on a certain number of PEs must correspond to runs where the time required by all PEs to reach the same error is greater than 0.3-0.4s.
- The last consideration is related to the genetic convergence. Simulation cannot last too long because after a certain time the genetic phase converges and no significant improvements are reachable in a reasonable time. Too long simulations with a number of PEs with a low P_{p,c} would imply very high artificial speedups.

For these two reasons the simulations using one p233 were chosen to last 300s, 150 and 75s.

Figure 1.23 clearly states that the implementation of GEFREX gains significantly in performance when many PEs are used. Given that the network is always utilized less than 10% of its maximum possibility the results are surprising: PARGEFREX is particularly suited for commodity supercomputers rather than very expensive servers with few processors.

Figure 1.23 confirms our discussion regarding too long simulations. If one p233 is used and the simulations last for 300s the speedup is particularly high: almost 450! This phenomenon is due to the fact that after 100-200s all the simulations converge and do not succeed in improving significantly. If we evaluated the average error when the simulation time was greater we would have a huge speedup, because the error would be almost identical to that found in 300s. Simulations using a p233 that last for 75s and 150s are more suited to evaluating the speedup.

The reader can see that the speedup is always greater than one. This fact implies a clear concept: the use of several PEs rather than only one permits the finding, on average, of very low learning errors. It is very improbable to find the same error with only one PE even if many very long simulations are launched. In this sense we can say that PARGEFREX is more effective than GEFREX.

To understand how important inter-slave communication is, PARGEFREX was used avoiding any exchange of individuals. Table 1.14 shows the results obtained when all PEs are used and the CT criterion was chosen with the simulation times fixed respectively to 0.5, 1.2 and 4 seconds. The last column reports the time that would be needed in the case of a migration time of 0.1s. There is a clear advantage permitting migration. With the fastest simulation the advantage is less evident in comparison to other cases, but it needs to be underlined that in this case the simulation time is almost all constituted by the neuro-phase and the genetic phase, where migration is allowed, is very short.

| t' (s) | e (RMNSE %) | Runs | t(e) (s) |
|---|---|---|---|
| 0.5 | 3.41779 | 88 | 0.41 |
| 1 | 3.39518 | 128 | 0.59 |
| 2 | 3.31133 | 318 | 1.50 |
| 4 | 3.23319 | 528 | 3.02 |

Table 1.14 Results obtained when all PEs are used and no exchange of data among slaves is permitted

| PEs | t' (s) | Num. procs | Runs | Improvement |
|---|---|---|---|---|
| 1 p233 | 75 | 5 | 88 | +27% |
| 1 p233 | 75 | 10 | 251 | +83% |
| all | 2 | 5 | 252 | +85% |
| all | 2 | 10 | 328 | +117% |

Table 1.15 Improvement as function of the number of processes per node and number of PEs

Further studies will investigate the optimal migration rate.

The last table 1.15 shows the behavior of PARGEFREX when more slaves are launched on the same PE. The first two rows show the results when PARGEFREX is launched using only one p233, but 5 and 10 slaves are spawned respectively. The last two refer to all PEs. The CE termination criterion was used. The simulation time is reported in column 3. The last column reports the percent improvement obtained in respect of the same simulation when only one slave is spawned per PE (see Table 1.13 to get mono-slave results). The results obtained show that more processes per PE imply greater performance. Moreover, this increase is more evident when the number of PEs used increases, too. Further studies will deal with this phenomenon.

## 1.5 References

[1] E.Shragowitz, J.Y.Lee, and Q.Kang, “Application of Fuzzy in Computer-Aided VLSI Design,” IEEE Transactions on Fuzzy Systems, vol. 6, pp. 163–172, Feb. 1998.

[2] J.Yen and N.Pfluger, “A Fuzzy Logic Based Extension to Payton and Rosenblatt’s Command Fusion Method for Mobile Robot Navigation,” IEEE Transactions on Systems, Man and Cybernetics, vol. 25, pp. 971–978, June 1995.

[3] H.R.Boem and H.S.Cho, “A Sensor-Based Navigation for a Mobile Robot Using Fuzzy Logic and Reinforcement Learning,” IEEE Transactions on Systems, Man and Cybernetics, vol. 25, pp. 464–477, Mar. 1995.

[4] K.Arakawa, “Fuzzy Rule-Based Signal Processing and Its Application to Image Restoration,” IEEE Journal on Selected Areas in Communications, vol. 12, pp. 1495–1502, Dec. 1994.

[5] G.V.Russo, U.Becciani, C.Caligiore, L.Lo Nigro, D.Lo Presti, S.Panebianco, L.Pappalardo, C.Petta, N.Randazzo, S.Reito, and M.Russo, “Smart Readout of Silicon Drift Detectors using ON-LINE Fuzzy Logic,” Nuclear Instruments & Methods in Physics Research - Section A, vol. 443, pp. 478–502, 2000.

[6] M.Russo, N.A.Santagati, and E.Lo Pinto, “Medicinal Chemistry and Fuzzy Logic,” Information Sciences, vol. 105/1-4, pp. 299–314, May 1998.

[7] Proceedings of the 21st International Conference on Industrial Electronics, Control and Instrumentation, 1995.

[8] C.T.Lin and C.S.G.Lee, “Neural-Network-Based Fuzzy Logic Control and Decision System,” IEEE Transactions on Computers, vol. 40, pp. 1320–1336, Dec. 1991.

[9] C.J.Lin and C.T.Lin, “Reinforcement Learning for an ART-Based Fuzzy Adaptive Learning Control Network,” IEEE Transactions on Neural Networks, vol. 7, pp. 709–731, May 1996.

[10] M.Grabish and F.Dispot, “A Comparison of Some Methods of Fuzzy Classification on Real Data,” in Proc. 2nd Int. Conf. on Fuzzy Logic and Neural Networks (IIZUKA’92), (Iizuka, Japan), pp. 659–662, July 1992.

[11] A.Lotfi and A.C.Tsoi, “Learning Fuzzy Inference Systems Using an Adaptive Membership Function Scheme,” IEEE Transactions on Systems, Man and Cybernetics – Part A, vol. 26, pp. 326–331, Apr. 1996.

[12] K.M.Lee, D.H.Kwak, and H.Lee-Kwang, “Fuzzy Inference Neural Network for Fuzzy Model Tuning,” IEEE Transactions on Systems, Man and Cybernetics – Part A, vol. 26, pp. 637–645, Aug. 1996.

[13] C.L.Karr and E.J.Gentry, “Fuzzy Control of pH Using Genetic Algorithms,” IEEE Transactions on Fuzzy Systems, vol. 1, pp. 46–53, Feb. 1993.

[14] S.H.Park, Y.H.Kim, Y.K.Choi, H.C.Cho, and H.T.Jeon, “Self-Organization of Fuzzy Rule Base Using Genetic Algorithms,” in Proc. 5th IFSA Congress, (Seoul, Korea), pp. 881–886, July 1993.

[15] A.Homaifar and E.McCormick, “Simultaneous Design of Membership Functions and Rule Sets for Fuzzy Controllers Using Genetic Algorithms,” IEEE Transactions on Fuzzy Systems, vol. 3, pp. 129–139, May 1995.

[16] T.Hashiyama, T.Furuhashi, and Y.Uchikawa, “A Creative Design of Fuzzy Logic Controller Using a Genetic Algorithm,” Advances in Fuzzy Systems, vol. 7, pp. 37–48, 1997.

[17] K.C.C.Chan, V.Lee, and H.Leung, “Generating Fuzzy Rules for Target Tracking Using a Steady-State Genetic Algorithm,” IEEE Transactions on Evolutionary Computation, vol. 1, pp. 189–200, Sept. 1997.

[18] M.Russo, “FuGeNeSys: A Fuzzy Genetic Neural System for Fuzzy Modeling,” IEEE Transactions on Fuzzy Systems, vol. 6, pp. 373–388, Aug. 1998.

[19] G.H.Golub and C.F.Van Loan, Matrix Computations. Baltimore and London: The Johns Hopkins University Press, 1996.

[20] M.Figueiredo, F.Gomides, A.Rocha, and R.Yager, “Comparison of Yager’s Level Set Method for Fuzzy Logic Control with Mamdani and Larsen Methods,” IEEE Transactions on Fuzzy Systems, vol. 1, no. 2, pp. 156–159, 1993.

[21] Y.Lin and G.A.Cunningham III, “A New Approach to Fuzzy-Neural System Modeling,” IEEE Transactions on Fuzzy Systems, vol. 3, pp. 190–198, May 1995.

[22] M.A.Lee and H.Takagi, “Integrating Design Stages of Fuzzy Systems Using Genetic Algorithms,” in Proc. IEEE Int. Conf. on Fuzzy Systems 1993, (San Francisco, California), pp. 612–617, 1993.

[23] H.Ishibuchi, K.Nozaky, and H.Tanaka, “Distributed Representation of Fuzzy Rules and Its Application to Pattern Classification,” Fuzzy Sets and Systems, vol. 52, pp. 21–32, 1992.

[24] H.Ishibuchi, K.Nozaki, N.Yamamoto, and H.Tanaka, “Selecting Fuzzy If-Then Rules for Classification Problems Using Genetic Algorithms,” IEEE Transactions on Fuzzy Systems, vol. 3, pp. 260–270, Aug. 1995.

[25] M.Russo, Metodi Hardware e Software per Logiche di Tipo non Tradizionale. PhD thesis, University of Catania, Catania, Italy, Feb. 1996. Ph.D. thesis in Italian.

[26] K.Liano, “Robust Error Measure for Supervised Neural Network Learning with Outliers,” IEEE Transactions on Neural Networks, vol. 7, pp. 246–250, Jan. 1996.

[27] C.Petta, G.V.Russo, B.Batyunya, C.Caligiore, D.Lo Presti, S.Panebianco, N.Randazzo, S.Reito, M.Russo, and A.Zinchenko,
