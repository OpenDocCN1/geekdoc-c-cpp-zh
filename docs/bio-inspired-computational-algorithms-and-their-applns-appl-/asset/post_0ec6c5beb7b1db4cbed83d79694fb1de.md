
![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_376_0.png)

Fig. 15. Temporal evolution of resting macrophages with $A(0) = 20$ and for distinct values of $\lambda_{N|A}$.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_376_1.png)

Fig. 16. Temporal evolution of activated macrophages with $A(0) = 20$ and for distinct values of $\lambda_{N|A}$.

(Muraille et al. (1996)). Klein (1980) presents and compares three mathematical models of B cell differentiation and proliferation.

ImmSim (Bezzi et al. (1997); Celada & Seiden (1992)) is a simulator of the HIS that implements the following mechanisms: immunological memory, affinity maturation, effects of hypermutation, autoimmune response, among others. CAFISS (a Complex Adaptive Framework for Immune System Simulation) (Tay & Havar (2005)) is a framework used for modelling the immune system, particularly HIV attack. SIMMUNE (Meier-Schellersheim & Mack (1999)) allows users to model cell biological systems based on data that describes cellular behaviour on distinct scales. Although it was developed to simulate immunological phenomena, it can be used in distinct domains. A similar tool is CyCells (Warrender (2004)), designed to study intercellular relationships.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_377_0.png)

Fig. 17. Temporal evolution of cytokines with $A(0) = 40$ for distinct values of $\lambda_{N|A}$.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_377_1.png)

Fig. 18. Temporal evolution of neutrophils with $A(0) = 40$ for distinct values of $\lambda_{N|A}$.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_377_2.png)

Fig. 19. Temporal evolution of LPS with $A(0) = 40$ for distinct values of $\lambda_{N|A}$.

As future works, we plan to implement a more complete mathematical model including, for example, new cells (Natural Killer, dendritic cells and the complement system), others proinflammatory cytokines, anti-inflammatory cytokine, molecules and others processes involved in the immune responses.

## 9. Acknowledgement

The authors would like to thank FAPEMIG, CNPq (479201/2010-2), CAPES and UFJF for supporting this study.

## 10. References

- Bezzi, M., Celada, F., Ruffo, S. & Seiden, P. E. (1997). The transition between immune and disease states in a cellular automaton model of clonal immune response, *Physica A: Statistical and Theoretical Physics* 245(1-2): 145 – 163.
    URL: http://www.sciencedirect.com/science/article/pii/S0378437197000964
- Celada, F. & Seiden, P. E. (1992). A computer model of cellular interactions in the immune system, *Immunology Today* 13(2): 56 – 62.
    URL: http://www.sciencedirect.com/science/article/pii/016756999290108M
- Day, J., Rubin, J., Vodovotz, Y., Chow, C. C., Reynolds, A. & Clermont, G. (2006). A reduced mathematical model of the acute inflammatory response ii. capturing scenarios of repeated endotoxin administration, *J Theor Biol* 242(1): 237–256.
    URL: http://dx.doi.org/10.1016/j.jtbi.2006.02.015
- de Waal Malefyt, R., Abrams, J., Bennett, L., Figdor, C. & de Vries, J. (1991). Interleukin 10 (IL-10) inhibits cytokine synthesis by human monocytes: an autoregulatory role of IL-10 produced by monocytes, *J Exp Med* 174(5): 1209–20.
    URL: http://dx.doi.org/10.1084/jem.174.5.1209
- Kirschner, D. (1999). Dynamics of co-infection with M. tuberculosis and HIV-1, *Theoretical Population Biology* 55(1): 94 – 109.
    URL: http://www.sciencedirect.com/science/article/pii/S004058099891382X
- Goutelle, S., Maurin, M., Rougier, F., Barbaut, X., Bourguignon, L., Ducher, M. & Maire, P. (2008). The hill equation: a review of its capabilities in pharmacological modelling, *Fundamental & Clinical Pharmacology* 22(6): 633–648.
    URL: http://dx.doi.org/10.1111/j.1472-8206.2008.00633.x
- Janeway, C., Murphy, K. P., Travers, P., Walport, M. & Janeway, C. (2001). *Immunobiology*, 5th edn, Garland Science, New York and London.
- Keener, J. & Sneyd, J. (1998). *Mathematical physiology*, Springer-Verlag New York Inc., New York, NY, USA.
- Klein, P. (1980). Mathematical models of antibody response, *Folia Microbiologica* 25: 430–438. 10.1007/BF02876697.
    URL: http://dx.doi.org/10.1007/BF02876697
- Kumar, R., Clermont, G., Vodovotz, Y. & Chow, C. C. (2004). The dynamics of acute inflammation, *Journal of Theoretical Biology* 230(2): 145–155.
- Zhang, B., Hirahashi, J., Cullere, X. & Mayadas, T. N. (2003). Elucidation of molecular events leading to neutrophil apoptosis following phagocytosis, *The Journal of Biological Chemistry* 278: 28443–28454.

## A Stochastically Perturbed Particle Swarm Optimization for Identical Parallel Machine Scheduling Problems

Mehmet Sevkli¹ and Aise Zulal Sevkli²

¹King Saud University, Faculty of Engineering, Department of Industrial Engineering, Riyadh

²King Saud University, College of Computer and Information Sciences, Department of Information Technology, Riyadh, Kingdom of Saudi Arabia

### 1. Introduction

Identical parallel machine scheduling (PMS) problems with the objective of minimizing makespan (C<sub>max</sub>) is one of the well known NP-hard [1] combinatorial optimization problems. It is unlikely to obtain optimal schedule through polynomial time-bounded algorithms. Small size instances of PMS problem can be solved with reasonable computational time by exact algorithms such as branch-and-bound [2, 3], and the cutting plane algorithm [4]. However, as the problem size increases, the computation time of exact methods increases exponentially. On the other hand, heuristic algorithms generally have acceptable time and memory requirements, but do not guarantee optimal solution. That is, a feasible solution is obtained which is likely to be either optimal or near optimal. The well-known longest processing time (LPT) rule of Graham [5] is a sort of so called list scheduling algorithm. It is known that the rule works very well when makespan is taken as the single criterion [6]. Later, Coffman et al. [7] proposed MULTIFIT algorithm that considers the relation between bin-packing and maximum completion time problems. Yue [8] showed that the MULTIFIT heuristic is not guaranteed to perform better than LPT for every problem. Gupta and Ruiz-Torres [9] developed a LISTFIT algorithm that combines the bin packing method of the MULTIFIT heuristic with multiple lists of jobs. Min and Cheng [10] introduced a genetic algorithm (GA) that outperformed simulated annealing (SA) algorithm. Lee et al. [11] proposed a SA algorithm for the PMS problems and compared their results with the LISTFIT algorithm. Tang and Luo [12] developed a new iterated local search (ILS) algorithm that is based on varying number of cyclic exchanges.

Particle swarm optimization (PSO) is based on the metaphor of social interaction and communication among different species in nature, such as bird flocking and fish schooling. It is different from other evolutionary methods in a way that it does not use the genetic operators (such as crossover and mutation), and the members of the entire population are maintained throughout the search procedure. Thus, information is socially shared among

### 2.2 Solution representation and lower bound

The solution for the PMS problem is represented as a permutation of integers Π={1,..., n} where Π defines the processing order of the jobs. As mentioned in the text above, three versions of the PSO algorithm are compared in terms of solution quality and CPU time.

In continuous based PSO by Tasgetiren et al. [17], PSO<sub>SPV</sub>, particles themselves do not represent permutations. Instead, the SPV rule is used to derive a permutation from the position values of the particle. In discrete PSO by Pan et al. [21] and the proposed algorithm (SPPSO), on the other hand, the particles represent permutations themselves.

| Jobs | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|
| p<sub>i</sub> | 7 | 7 | 6 | 6 | 5 | 5 | 4 | 4 | 4 |

Table 1. An example of 9-job × 4-machine PMS problem

For all of the three algorithms, the process of finding makespan value for a particle can be illustrated by an example. Namely, let’s assume a permutation vector of Π= {1 8 3 4 5 6 7 2 9}. By considering 4 parallel machines and 9 jobs, whose processing times are given in Table 1, the makespan value of the given vector is depicted in Figure 1.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_384_0.png)

According to the schedule, each value of the vector is iteratively assigned to the most available machine. First four elements of the permutation vector (1,8,3,4) are assigned to the four machines respectively. The remaining jobs are assigned one by one to the first machine available. For instance, 5 goes to second machine (M2), since it is the first machine released. If there is more than one available machine at the time, the job will be assigned randomly (ties can be broken arbitrarily). The makespan value of the given sequence is C<sub>max</sub>(Π)=14, as can easily be seen in figure 1.

The lower bound for P | C<sub>max</sub> is calculated as follows [22]:

LB(C<sub>max</sub>) = max { ⌈(1/m) Σ<sub>i=1</sub><sup>m</sup> p<sub>i</sub>⌉ ; max<sub>i</sub> {p<sub>i</sub>} } (3)

It is obtained by assuming that preemption is not allowed. If C<sub>max</sub>(Π)=LB(C<sub>max</sub>), the current solution(Π) is optimum. So, lower bound will be used as one of the termination criteria
