
![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_129_0.png)

Fig. 10. The evolutions of CGA, SCQGA and QIGA

| Parameter | CGA | SCQGA | QIGA |
|---|---|---|---|
| Global time | 73.990 s | 38.599 s | 19.263 s |
| Self time | 2.447 s | 1.417 s | 1.390 s |
| Evaluation time | 59.561 s | 31.536 s | 11.750 s |
| Calls of evaluation function | 25200 | 19200 | 4836 |
| Ratio between evaluation and global time | 80.5 % | 81.7 % | 60.9 % |
| Number of generations | 300 | 300 | 300 |
| Successful runs in 10 attempts (with fitness of 100%) | 7 | 6 | 6 |

Table 1. A comparison between CGA, SCQGA and QIGA

Unfortunately, the number of successful runs in 300 generations is only in the order of 70% for CGA, and 60% for the rest two algorithms. It occurs due to the constraint that only 100% in fitness evaluation is accepted. In other applications, this constraint may be not critical.

## 6. Conclusion

In this chapter we did a summary outline of GAs and discussed some possible applications. We presented three extrinsic evolutionary designs of digital circuits at gate level using GAs.

Future research must be done in this area. Firstly it is important to find a better representation of the circuit in chromosomes, because complex functions need a great number of architecture bits, which directly influences the GA search space. EHW successfully succeeds only when fitness reaches 100% and in huge search spaces this condition may be not always possible. This is the main reason that for the time being the complexity of evolved circuits is so far small. In our opinion, conclusion drawn in the paper (Yao & Higuchi, 1999) is still available: “EHW research needs to address issues, such as scalability, online adaptation, generalization, circuit correctness, and potential risk of evolving hardware in a real physical environment. It is argued that a theoretical foundation of EHW should be established before rushing to large-scale EHW implementations”.

Recently appeared the idea of hybridization of a GA with elements of quantum computation (Han & Kim, 2002; Han, 2003). We have proposed a new quantum inspired genetic algorithm (QIGA) considerably faster than other similar algorithms, based on the idea of introducing a new parameter, which we called the probability of collapse, and to initiate the collapse of the quantum chromosome in order to generate a conventional population of chromosomes from time to time, and not each generation, as usually is done. We believe that some improvements in this method may be found in a future research, by establishing of a new method of updating the quantum chromosome from the current generation to the next one. Finally, some hybridization techniques may be useful for new quantum inspired evolutionary algorithms. (Rubinstein, 2001) used Genetic Programming to evolve quantum circuits with various properties, and (Moore & Venayagamoorthy, 2005) has developed an algorithm inspired from quantum evolution and Particle Swarm to evolve conventional combinational logic circuits.

## 7. References

- Bentley, P. J. & Corne, D. W. (Ed(s).). (2002). Creative Evolutionary Systems, Academic Press, ISBN: 1-55860-673-4, San Francisco, USA
- Bilchev, G. & Parmee, I. (1996). Constraint Handling for the Fault Coverage Code Generation Problem: An Inductive Evolutionary Approach, Proceedings of 4-th Conference on Parallel Problem Solving from Nature (PPSN IV), pp. 880-889, Berlin, September 1996
- Burda, I. (2005). Introduction to Quantum Computation, Universal Publishers, ISBN: 1-58112-466-X, Boca Raton, Florida, USA
- Forbes, N. (2005). Imitation of Life. How Biology Is Inspiring Computing, MIT Press, ISBN: 0-262-06241-0, London, England
- Han, K. H. & Kim, J. H. (2002). Quantum-Inspired Evolutionary Algorithm for a Class of Combinatorial Optimization, IEEE Transactions on Evolutionary Computation, vol.6, no.6, (December 2002), pp. 580-593, ISSN 1089-778X
- Han, K. H. (2003). Quantum-Inspired Evolutionary Algorithm, Ph.D. dissertation, Department of Electrical Engineering and Computer Science, Korea Advanced Institute of Science and Technology, Korea, 2003
- Haupt, R. L. & Haupt, S. E. (2004). Practical Genetic Algorithms (second edition), Wiley-Interscience, ISBN: 0-471-45565-2, New-Jersey, USA
- Higuchi, T.; Liu, Y. & Yao, X. (Ed(s).). (2006). Evolvable Hardware, Springer-Verlag, ISBN-13: 978-0387-24386-3, New-York, USA
- Iba, H.; Iwata, M. and Higuchi, T. (1996). Machine Learning Approach to Gate-Level Evolvable Hardware. Proceedings of the First International Conference on Evolvable Systems ICES'96, pp.327-343, Tsukuba, Japan, October 1996
- Mazumder, P. & Rudnick, E. M. (1999). Genetic Algorithms for VLSI Design, Layout & Test Automation, Prentice Hall PTR, ISBN: 0-13-011566-5, Upper Saddle River, New Jersey, USA
- Michalewicz, Z. (1996). Genetic Algorithms + Data Structures = Evolution Programs (third edition), Springer-Verlag, ISBN: 3-540-58090-5, New-York, USA
- Mitchell, M. (1997). An Introduction to Genetic Algorithms (third printing), MIT Press, ISBN: 0-262-13316-4, London, England
- Moore, Ph. & Venayagamoorthy, G. K. (2005). Evolving Combinational Logic Circuits using a Hybrid Quantum Evolution and Particle Swarm Inspired Algorithm, Proceedings of the 2005 NASA/DoD Conference of Evolution Hardware EH'05, pp. 97-102, 2005
- Popa, R.; Aiordachioaie, D. & Nicolau, V. (2002). Multiple Hybridization in Genetic Algorithms, The 16-th European Meeting on Cybernetics and Systems Research EMCSR'2002, pp.536-541, ISBN 3-85206-160-1, Vienna, Austria, April 2-5, 2002
- Popa, R. (2004). Evolvable Hardware in Xilinx XC3R3064 CPLD, IFAC Workshop on Programmable Devices and Systems, PDS 2004, pp. 232-237, ISBN: 83-908409-8-7, Cracow, Poland, November 18-19, 2004
- Popa, R.; Aiordachioaie, D. & Sirbu, G. (2005). Evolvable Hardware in Xilinx Spartan 3 - FPGA, 2005 WSEAS International Conference on Dynamical Systems and Control, pp. 66-71, ISBN 960-8457-37-8, Venice, Italy, November 2-4, 2005
- Popa, R.; Nicolau, V. & Epure, S. (2010). A New Quantum Inspired Genetic Algorithm for Evolvable Hardware, 3rd International Symposium On Electrical and Electronics Engineering ISEEE 2010, pp. 64-69, ISBN: 978-1-4244-8407-2, Galati, Romania, September 16-18, 2010 (in IEEE Xplore Digital Library, DOI 10.1109/ISEEE.2010.5628539)
- Rubinstein, B. I. P. (2001). Evolving Quantum Circuits using Genetic Programming, Proceedings of the 2001 Congress on Evolutionary Computation, CEC2001, pp.114-121, IEEE Press, 2001
- Schöneburg, E.; Heinzmann, F. & Feddersen, S. (1994). Genetische Algorithmen und Evolutionsstrategien. Eine Einführung in Theorie und Praxis der simulierten Evolution, Addison-Wesley, ISBN: 5-89319-493-2, München, Germany
- Sivanandam, S. N. & Deepa, S. N. (2008). Introduction to Genetic Algorithms, Springer-Verlag, ISBN: 978-3-540-73189-4, India
- Wong, K. P. & Wong, Y. W. (1994). Development of Hybrid Optimisation Techniques Based on Genetic Algorithms and Simulated Annealing, Workshop on Evolutionary Computation (AI'94), pp. 127-154, Armadale, Australia, November 1994
- Yao, X. & Higuchi, T. (1999). Promises and Challenges of Evolvable Hardware, IEEE Transactions on Systems, Man, and Cybernetics – Part C: Applications and Reviews, Evolutionary Computation, vol.29, no.1, (February 1999), pp. 87-97, ISSN 1094-6977
- Zhou, S. & Sun, Z. (2005). A New Approach Belonging to EDAs: Quantum-Inspired Genetic Algorithm with Only One Chromosome, International Conference on Natural Computing, ICNC2005, pp. 141-150, LNCS 3612, Springer-Verlag, 2005

## Part 2

### New Applications of Genetic Algorithm

## Tune Up of a Genetic Algorithm to Group Documentary Collections

José Luis Castillo Sequera
University of Alcalá, Department of Computer Science, Madrid
Spain

### 1. Introduction

Both in industry and science there are some real problems regarding the optimization of difficult solution characterized by computational complexity, because the available exact algorithms are inefficient or simply impossible to implement. The metaheuristics (MHs) are a family of approximate methods of general purpose consisting in iterative procedures that guide heuristics, intelligently combining different concepts to explore and exploit properly the search space [12]. Therefore, there are two important factors when designing MHs : intensification and diversification. The diversification generally refers to the ability to visit many different regions of search space, while intensification refers to the ability to obtain high quality solutions in these regions. A search algorithm must achieve a balance between these two factors so as to successfully solve the problem addressed.

On the other hand, Information Retrieval (IR) can be defined as the problem of information selection through a storage mechanism in response to user queries [3]. The Information Retrieval Systems (IRS) are a class of information systems that deal with databases composed of documents, and process user's queries by allowing access to relevant information in an appropriate time interval. Theoretically, a document is a set of textual data, but technological development has led to the proliferation of multimedia documents [4].

Genetic Algorithms (GAs) are inspired by MHs in the genetic processes of natural organisms and in the principles of natural evolution of populations [2]. The basic idea is to maintain a population of chromosomes, which represent candidate solutions to a specific problem , that evolve over time through a process of competition and controlled variation. One of the most important components of GAs is the crossover operator [7]. Considering all GA must have a balance between intensification and diversification that is capable of augmenting the search for the optimal, the crossover operator is often regarded as a key piece to improve the intensification of a local optimum. Besides, through the evolutionary process, every so often there are species that have undergone a change (mutation) of chromosome, due to certain evolution factors, as the mutation operator is a key factor in ensuring that diversification, and finding the optimum feasible regions.

Efficiently assigning GA parameters optimizes both the quality of the solutions and the resources required by the algorithm [13]. This way, we can obtain a powerful search
