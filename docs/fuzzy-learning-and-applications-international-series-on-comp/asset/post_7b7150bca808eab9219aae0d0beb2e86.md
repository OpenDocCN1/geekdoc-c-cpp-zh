
## 8.8.2 TSP by Szu’s Energy Function

The fuzzy logic-based algorithm was applied to a TSP featuring 15 cities with random distances between them.

The minimum distance in the scenario was 0.05, so the LowerBound was set to 0.75. The Tolerance was set to 10, δ to 5 and ε to 0.01.

The sets of IterDelta, IterMaxGood and PercIterMaxGood values are the same shown in (8.26). This choice was made to assess the influence of IterDelta on the quality of the solution, as done in the previous section.

On the basis of this set of parameters, the fuzzy-logic algorithm gave the HCs:

```
HCs = { A = B = 317
        C = 888
        D = 766 } (8.31)
```

Unfortunately in [5] Szu did not specify the set of HCs that he used in his energy function. For this reason we can not compare the solutions obtained using (8.31) with those featured by the original Szu’s work for the same scenarios, as done in the previous section with the Hopfield and Tank’s solution. The comparison between the two approaches may be done only on the basis of the percentage of optimal solutions obtained in TSPs featuring certain number of cities, as only this information is available in the Szu’s work [5] and in [35].

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_285_0.png)

## Figure 8.12 Quality of solution

In Fig. 8.12 the percentage of optimal solutions obtained with the set of coefficients (8.31) is shown, considering TSPs featuring 5, 10, 15, 20, 25, 30 and 40 cities.

As said in the previous section, 10 different random distance scenarios were considered for each TSP (i.e., for each number of cities) and for each distance scenario 10 consecutive neural solutions were found. For each TSP, Fig. 8.12 shows the average percentage of optimal solutions found in 10 consecutive neural iterations. As the TSP is a NP-hard optimization problem, the optimal solutions for very complicated problems featuring a number of cities greater than 15 could not be calculated. For this reason the goodness of the solution provided by the Hopfield network related to TSPs featuring number of cities greater than 15 was evaluated on the basis of the smallest observed tour length, as defined in [36].

As can be seen from Fig. 8.12, now the average values of optimal solution percentage features higher values if compared with those shown in Fig. 8.11, highlighting the important role played by the energy function.

From Fig. 8.12 it is clear that the percentage of optimal solution ranges from 60% to 90%, featuring high values for very complicated problems (20–40 cities), too. This is a very remarkable result, above all on account of the high percentage values obtained for large TSPs. For similar complex problems the Szu's approach seldom gives close-to-optimal solution, as is reported in [5] and [35].

## 8.8.3 FMS Performance Optimization

No example of FMS performance optimization solved by the Hopfield neural network is available in literature. For this reason the authors can not compare the performance of the neural solution obtained using the coefficients found by the fuzzy approach versus the performance obtained using some other set of coefficients. What it is possible to say is that the choice of the values of the HCs was very hard. By using an heuristic approach (i.e., by manually varying the coefficients), the authors were not able to find a set of coefficients which guarantee valid solutions. The use of the Fuzzy method described in the previous section allowed to identify a set of coefficients which guarantee a high percentage of valid solutions. The set of coefficients that were found is

```
HCs = { A = 80
B = 385
C = 295 } (8.32)
```

and the percentage of valid and optimal solution can be assessed about at 25%.

## 8.9 Conclusions

The chapter has presented the use of fuzzy inferences for the automatic determination of the coefficients of the energy function linked to the surrounding conditions of the problem to be solved. Until now the only methodology known for this tuning is manual heuristic search, essentially based on the know-how of the human operator. This procedure is not only very time-consuming but it cannot assure optimal solutions. In fact, the set of coefficients determined could provide solutions which are very far from the optimal solution to the problem.

The chapter has focused on the possibility of using the automatic HC search algorithm to reach two different goals. As has been stressed, it is, in fact, possible to force the automatic search towards coefficients which provide robust or good-quality solutions.

This feature is particularly interesting as it allows us to meet the different requirements that arise when optimization methods are used. It is possible to find HCs that provide optimal solutions or coefficients which allow good solutions but of not such high quality, in exchange for a lower computational effort.

The results reported in the chapter effectively show that the approach proposed features a search for the set of coefficients which guarantees valid solutions very close to the global minima of the energy function, or ones which guarantee very robust solutions. The robustness and quality features obtained were much higher than those provided by classical heuristic approaches.

Due to the inherent features of this automatic tool based on fuzzy logic, we believe that it greatly enhances the real use of the Hopfield network for solving very complex optimization problems.

*Networks*, vol. 7, no. 5, pp. 1272–1285, 1996.

[15] T.Yamakawa, “Stabilization of an Inverted Pendulum by a High-Speed Fuzzy Logic Controller Hardware System,” *Fuzzy Sets and Systems*, pp. 161–180, 1989.

[16] F.Beritelli, S.Casale, and M.Russo, “Robust Phase Reversal Tone Detection Using Soft Computing,” in *IEEE Proceedings of the Third International Symposium on Uncertainty Modeling Analysis and Annual Conference of the North American Fuzzy Information Processing Society, ISUMA-NAFIS ’95*, (College Park, Maryland, USA), pp. 589–594, Sept. 1995.

[17] M.Russo, *Metodi Hardware e Software per Logiche di Tipo non Tradizionale*. PhD thesis, University of Catania, Catania, Italy, Feb. 1996. Ph.D. thesis in Italian.

[18] V.Catania, N.Fiorito, M.Malgeri, and M.Russo, “A Framework for Codesign based on Fuzzy Logic and Genetic Algorithms,” in *Proceedings of the Eighth International Conference on Industrial and Engineering Applications of Artificial Intelligence and Expert Systems, IEA/AEI ’95*, (Melbourne, Australia), pp. 797–804, June 1995.

[19] M.A.Cohen and S.G.Grossberg, “Absolute Stability of Global Pattern Formation and Parallel Memory Storage by Competitive Neural Networks,” *IEEE Transactions on Systems, Man and Cybernetics*, vol. 13, pp. 915–926, 1983.

[20] R.Hecht and Nielsen, *Neurocomputing*. Reading, MA: Addison-Wesley, first ed., 1990.

[21] J.J.Hopfield, “Neurons with Graded Response Have Collective Computational Properties Like Those of Two-State Neurons,” in *National Academy of Science*, pp. 3088–2092, May 1984.

[22] L. A.Zadeh, “Fuzzy Sets,” *Information and Control*, pp. 338–353, 1965.

[23] Y.Lin and G.A.Cunningham III, “A New Approach to Fuzzy-Neural System Modeling,” *IEEE Transactions on Fuzzy Systems*, vol. 3, pp. 190–198, May 1995.

June 1996.
[28] S.Cavalieri, “Application of Neural Networks to Factory Automation Performance Optimization,” in *Computational Engineering in Systems Applications, CESA 96*, (Lille, France), pp. 240–245, June 1996.
[29] S.Cavalieri, “A Novel Neural Network Model for the Performance Evaluation of Flexible Manufacturing Systems,” in *22nd Annual International Conference on Industrial Applications, IECON96*, (Taipei, Taiwan), Aug. 1996.
[30] J.R.Pimentel, *Communication Networks for Manufacturing*. Prentice-Hall international Editors, 1990.
[31] J.H.P.Hillion, “Performance Evaluation of Job-Shop Systems using Timed Event Graphs,” *IEEE Transaction on Automatic Control*, vol. 34, no. 1, pp. 3–9, 1989.
[32] R.Zurawski, “Petri Nets and Industrial Application: A Tutorial,” *IEEE Transaction on Industrial Electronics*, vol. 41, no. 6, pp. 915–926, 1994.
[33] G.M.Ajmone, G.Conte, *Performance Models of Multiprocessor Systems*. Computer System Series, 1986.
[34] X.S.Lafti, J.M.Proth, “Optimization of Invariant Criteria for Event Graphs,” *IEEE Transaction on Automatic Control*, vol. 37, no. 5, pp. 547–555, 1992.
[35] NeuralWare, *Neural Computing: A Technology Handbook for Professional II/PLUS and NeuralWorks Explorer*, pp. 191–208. NeuralWare, Inc. Technical Publications Group, 202 Park West Drive, Pittsburg, PA 15275, USA: NeuralWare, Inc., 1995.
[36] E.Aarts and Jan Korst, *Simulated Annealing and Boltzmann Machines*, ch. 9, pp. 153–179. John Wiley & Sons, 1990.
