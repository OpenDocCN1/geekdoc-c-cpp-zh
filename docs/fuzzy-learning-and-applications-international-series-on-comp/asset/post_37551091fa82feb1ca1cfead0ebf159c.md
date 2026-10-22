
## DEDICATION

This book is dedicated to my wife

*Marco Russo*

## CREDITS

Figures 4.1, 4.2, 4.7, 4.8 and Tables 4.4 and 4.5 — From Alfonso, D., Masulli, F., and Sperduti, A., Competitive learning in a classifier based on an adaptive fuzzy system, in Proc. Int. ICSC Symp. Ind. Intel. Automation and Soft Computing, Anderson, P.G. and Warwick, K., Eds., Academic Press, Alberta, Canada, 1996. With permission.

Figure 4.3 — From Masulli, F., Bayesian classification by feedforward connectionist systems, in Proc. Adv. Sch. Ital. Biomed. Phys. Assoc., Masulli, F., Morasso, P.G., and Schenone, A., Eds., World Scientific, Singapore, and Como, Italy, 1993, 145-162. With permission.

Figures 4.4 and 4.5 — From Giusti, N., Masulli, F., and Sperduti, A., Competitive and hybrid neuro-fuzzy models for supervised classification, in Proc. IEEE Int. Conf. Neural Networks, IEEE, Houston, 1997, 516-519. With permission.

Table 4.1 — From Masulli, F., Casalino, F., and Vannucci, F., Bayesian properties and performances of adaptive fuzzy systems in pattern recognition problems, in Proc. Eur. Conf. Artificial Neural Networks ICANN, Marinaro, M. and Morasso, P.G., Eds., Springer, Sorrento, Italy, 1994, 189-192. With permission.

Table 4.2 — From Casalino, F., Masulli, F., and Sperduti, A., Rule specialization and semantic phase transition in the adaptive fuzzy system, in Proc. ICSC Int. Symp. Fuzzy Logic, Steele, N.C., Eds., Academic Press, Millet Alberta, Canada and Zurich, Switzerland, 1995, B87-B92. With permission.

## 1
Evolutionary Fuzzy Learning

## Evolutionary Fuzzy Learning

Marco Russo
M.Russo is with INFN Section of Catania - ITALY and with the Dept. of Physics, Univ. of Messina, Contrada Papardo, Salita Sperone 31, 98166 ME 1.4 - ITALY. E-mails:
marco.russo@ai.unime.it,
marco.russo@ct.infn.it,
marco.russo@ieee.org

- Abstract................................................... 2
- 1.1 Introduction........................................... 2
- 1.2 Fuzzy knowledge representation................ 2
- 1.3 GEF REX................................................... 5
- General description • The evolution algorithm • Genetic coding • Crossover • The error • Output singletons • Hill climbing operator • The fitness function • GEF REX utilization • Comparisons • Computational complexity evaluation • A learning example with compressed learning patterns
- 1.4 PARGEF REX............................................... 33
- A brief review of GEF REX • The commodity supercomputer used • PARGEF REX description • Performance evaluation
- 1.5 References ............................................. 48

## Evolutionary Fuzzy Learning

## Abstract

This chapter presents the fusion of neural networks and genetic algorithms for fuzzy supervised learning. It is demonstrated that this approach is superior for tasks such as classification, function approximation, and time series prediction.

### 1.1 Introduction

Linguistic rules to describe systems are being used successfully in many application domains [1–7]. Fuzzy systems are very suitable to describe very complex systems where it is very difficult to give a mathematical description.

Until now, there has been no systematic procedure for the design of Fuzzy Logic (FL) systems. To overcome this problem some papers propose automatic methods to extract fuzzy rules using Neural Networks (NNs) [8,9], fuzzy clustering [10–12], genetic algorithms (GAs) [13–17], or GAs+NNs methods [18]. Some of these techniques generate fuzzy logic controllers [9,13,15,16]. Other methods are used for fuzzy classification, fuzzy function approximation, or time series prediction.

This chapter presents a hybrid GAs+NNs approach (called GEFREX, which stands for GEnetic Fuzzy Rule EXtractor) for fuzzy supervised learning. It is able to deal with tasks such as classification, function approximation, and time series prediction. Its main characteristic is the low number of parameters needed in the description of the systems learnt.

The chapter is divided into two parts. In the former we have included in detail GEFREX and its capabilities. In the latter the distributed version of GEFREX is explained. This new software has been called PARGEFREX and shows very interesting properties in finding very difficult minima of the error function.

### 1.2 Fuzzy knowledge representation

concerned, while WM is preferable in classification problems. Moreover, the WM generally has the advantage that the learnt knowledge base seems easier for a human to understand.

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_16_0.png)

Figure 1.1 A fuzzy system made up of only two rules with the two inputs X₁ and X₂ and the output Y₁. The two crisp inputs x₁ and x₂ are used contemporarily in all rules to evaluate the degrees of truth of all antecedents (αᵢᵣ). Then the degree of truth θᵣ of each rule is computed through a minimum operation. Finally, the output is obtained with a WS defuzzification.

Fig. 1.1 shows an example of calculation of a fuzzy inference made up of only two rules. This inference uses the WS and has only two inputs and one output.

### 1.3 GEFREX

#### 1.3.1 General description

The algorithm proposed is a GA. The genetic population is placed on a rectangular grid. The core of the algorithm foresees a number of iterations, each of them consisting of the choice of two parents, the generation of only one offspring and its re-insertion in the population. The genetic coding of the fuzzy rules involves only the premises of the rules. It will be demonstrated that in the least squares sense the best consequents can be found in a robust manner with a SVD algorithm regardless of whether or not the WS or the WM defuzzification is used.

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_17_0.png)

Figure 1.2 The GA used in GEFREX. Firstly, two parents are selected. Then, an offspring is generated. From the offspring the best consequents are computed. If the fitness improves the best value obtained so far, then the neuro hill climbing operator is used. Lastly, the individual is inserted in the population. The algorithm is repeated until the end criterion is met.

![](img/ffb89ef8c668ade3e6e47a9ee7de70e5_19_0.png)

Figure 1.3 The evolution algorithm used. Each generation consists of the choice of a subpopulation. After, inside the subpopulation, two parents and the worst individual are selected. Only one offspring is generated and mutated. It replaces the worst individual.

are selected from a deme with a given radius. The selection is preservative, elitist, steady-state, and fitness proportional [25], as was the previous tool FuGeNeSys.

In fine-grain models there are two types of selections: global and local. In this case, global selection is fitness-proportional and identifies the center of the subpopulation deme. In GEFREX this radius is one, i.e., the subpopulation is a 3 × 3 subgrid. Local selection uses the same selection method but only in the subpopulation deme. Two parents generate a single offspring using the customized crossover and mutation operators described below. Whenever an individual is generated with a fitness value higher than the best one obtained so far a hill climbing operator is used too. The generated offspring replaces the individual in the subpopulation with the lowest fitness value.

In [18] there is a study that shows that the hill climbing algorithm based

#### 1.3.3 Genetic coding

Fig. 1.4 shows the genetic coding in detail. Each individual consists of two parts. The first part involves the Gaussians of all antecedents. The second part is dedicated to the enable bits. The number of inputs I depends on the application fields, whereas the number of rules R has to be specified by the user of GEFREX. In the same way as a multilayer perceptron, where the number of neurons implies the performance during the learning phase, too few hidden neurons imply high error whereas too many imply overfitting; the number of rules must be fixed taking into account the complexity of the problem to be learned by GEFREX.

Once these quantities are fixed, the coding size is given too. In fact, at maximum R × I antecedents (one for each rule and for each input) are required. Two parameters for each antecedent are required (the center and the width related parameters shown in formula (1.1)). So, the first part of the GEFREX coding requires 2 × R × I real values. Instead, the second part requires only I bits. These bits are used when the feature selection option is enabled during the learning phase of GEFREX. In a first approximation, these last I bits, in respect of the bits required to code the antecedents, can be ignored. Afterwards, the genetic coding in GEFREX requires a number of bits proportional to the quantity R × I.

In the next sections of this chapter it will be demonstrated that the number of rules required is generally very small. That is, GEFREX needs fewer rules than previous works to reach the same learning error. Furthermore, GEFREX often reaches a lower error than previous work with a smaller number of rules. Besides, R is not tied to the number of inputs, but only to the complexity of the application itself.

The coding of the individuals is made as follows:

Binary genes: A string of I bits is associated to each individual. They represent the enabled inputs in the coded inference. More precisely if, for example, I = 4 and the string is {0,1,1,0}, it means that in the fuzzy inference the first and the fourth inputs are not present. In this case GEFREX does not consider the information related to these inputs.

Real genes: Each individual in the population is made up of a set of R × I FSs too. They are respectively the I FSs of the premise of the first rule, the second I FSs of the second rule, ...., and the last I FSs of the premise of the last rule. As the MFs of the input FSs
