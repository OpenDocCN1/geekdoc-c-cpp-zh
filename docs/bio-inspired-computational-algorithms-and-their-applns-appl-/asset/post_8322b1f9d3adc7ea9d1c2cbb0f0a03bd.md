
It is decreased again as soon as an improvement of the population occurs” (Sivanandam & Deepa, 2008).

Fast Messy Genetic Algorithm (FmGA) is a binary, stochastic, variable string length, population-based approach to solving optimization problems. The main difference between the FmGA and other genetic approaches is the ability of the FmGA to explicitly manipulate building blocks (BBs) of genetic material in order to obtain good solutions and potentially the global optimum. Some works, like (Haupt & Haupt, 2004), use only the term of Messy Genetic Algorithms (mGAs).

Finally, Independent Sampling Genetic Algorithms (ISGAs) are more robust GAs, which manipulate building blocks to avoid the premature convergence in a GA. Implicit parallelism and the efficacy of crossover are enhanced and the ISGAs have been shown to outperform several different GAs (Sivanandam & Deepa, 2008). Other classes of efficient GAs may be implemented for different specific applications.

## 5. Applications of Genetic Algorithms

“GAs have been applied in science, engineering, business and social sciences. Number of scientists has already solved many engineering problems using genetic algorithms. GA concepts can be applied to the engineering problem such as optimization of gas pipeline systems. Another important current area is structure optimization. The main objective in this problem is to minimize the weight of the structure subjected to maximum and minimum stress constraints on each member. GA is also used in medical imaging system. The GA is used to perform image registration as a part of larger digital subtraction angiographies. It can be found that GAs can be used over a wide range of applications” (Sivanandam & Deepa, 2008). GAs can also be applied to production planning, air traffic problems, automobile, signal processing, communication networks, environmental engineering and so on. In (Bentley & Corne, 2002), Evolutionary Creativity is discussed, using a lot of examples from music, art in general, architecture and engineering design. Evolutionary Electronics, both Analog and Digital, have been investigated in many publications (Bentley & Corne, 2002; Popa, 2004; Popa et al., 2005). (Higuchi et al., 2006) is a very good book on Evolvable Hardware.

Evolvable Hardware (EHW) is hardware built on software-reconfigurable Programmable Logic Devices (PLDs). In these circuits the logic design is compiled into a binary bit string and, by changing the bits, arbitrary hardware structures can be implemented instantly. The key idea is to regard such a bit string as a chromosome of a Genetic Algorithm (GA). Through genetic learning, EHW finds the best bit string and reconfigures itself according to rewards received from the environment (Iba et al., 1996).

In the rest of this section we present three applications in evolutionary design of digital circuits developed by the author, using GAs. First of them describes a method of synthesis of a Finite State Machine (FSM) in a Complex Programmable Logic Device (CPLD), using a standard GA. The other two applications use different techniques of hybridisation of a standard GA: first of them with two other optimisation techniques (inductive search and simulated annealing), to solve the Automatic Test Pattern Generation for digital circuits, a problem described in (Bilchev & Parmee, 1996), and the second one to improve the convergence of the standard GA in evolutionary design of digital circuits, using the new paradigm of Quantum Computation (Han & Kim, 2002).

### 5.1 Implementation of a FSM using a standard GA

This first example uses extrinsic hardware evolution, that is, uses a model of the hardware and evaluates it by simulation in software. The FSM represented in Figure 3 is a computer interface for serial communication between two computers. A transition from one state to another depends on only one of the 4 inputs x_i, i=1..4. The circuit has 4 outputs, each of them being in logic 1 only in a single state. The FSM has 6 states and has been presented in (Popa, 2004).

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_121_0.png)

Fig. 3. A FSM described as state transition graph and manual state assignment

With the state assignment given in Figure 3, the traditional design with D flip-flops gives the following equations for the excitation functions:

```
D2 = x3 · Q1 · Q0 + Q1 · Q0̅ + Q1̅ · Q0̅
D1 = x2 · Q1̅ · Q0 + x1 · Q0 + Q1 · Q0̅
D0 = x1 · Q0̅ · Q0̅ + x2 · Q1 · Q0 + Q1 · Q0̅
```

The output functions are given by the following equations:

```
y1 = Q1̅ · Q0
y2 = Q2̅ · Q1 · Q0̅
y3 = Q2 · Q1̅
y4 = Q2 · Q1
```

For the evolutionary design of this circuit we take into account that each boolean function has a maximum number of 5 inputs and a maximum number of 4 minterms. If we want to implement these functions in a PLD structure (an AND array and logic cells configurable as OR gate), then the number of fuse array links is 2·5·4=40, and we may consider this number as the total length of the chromosome (Iba et al., 1996).

Our GA is a standard one, with the population size of 30 chromosomes. One-point crossover is executed with a probability of 80% and the mutation rate is 2%. Six worse chromosomes are replaced each generation. The stop criterion is the number of generations.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_122_0.png)

Fig. 4. The evolution of the excitation functions of the computer interface

Figure 4 reflects the evolution of the circuit for the first 3 functions, called excitation functions, which generate the subcircuit A. However, this circuit is built from 3 independent circuits, each generating one output bit. Therefore, the evolution of a circuit with one output bit is repeated 3 times. The Y-axis is the correct answer rate. If it reaches 100%, then the hardware evolution succeeds.

In the same way, Figure 5 reflects the evolution of the circuit for the output functions, which generate the subcircuit B. The evolution succeeds after a smaller number of generations because the total search space is in this case much lower than in previous case (all the output functions have only 3 variables).

Evolution may provide some non-minimal expressions for these boolean functions, but minimization is not necessary for PLD implementations. The length of the chromosomes is greater than the optimal one, and the evolved equations are much more complicated than the given equations (1-7). The complete cost of the whole combinational circuit consists of 15 gates and 37 inputs for traditional design, and 30 gates and 102 inputs for evolutionary design.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_123_0.png)

Fig. 5. The evolution of the output functions of the computer interface

We have implemented both the traditional design and the evolved circuit in a real Xilinx XCR3064 CoolRunner CPLD by using the Xilinx ISE 6.1i software. In traditional design, that is using equations (1-7), the FSM used only 7 macrocells from a total number of 64 macrocells, 11 product terms from a total number of 224 product terms, and 7 function block inputs, from a total number of 160. Surprising is the fact that, although evolutionary design, with the same state assignment, provides more complicated equations, the implementation of this circuit in XCR3064XL CPLD also used 7 macrocells from a total number of 64, 10 product terms from a total number of 224, and 7 function block inputs, from a total number of 160. This is even a better result than in the preceding case, because the number of product terms is less with 1. Both implementations have used the same number of flip-flops (that is 3/64) and the same number of pins used like inputs/outputs (that is 9/32). We have preserved the state assignment of the FSM, and the subcircuits A and B are in fact pure combinational circuits. The interesting fact is that our GA has supplied a better solution than the one given by the minimization tool used for this purpose by the CAD software.

### 5.2 Multiple hybridization of a GA

Hybrid Genetic Algorithms (HGAs) combine the power of the GA with the speed of a local optimizer. Usually the GA finds the region of the optimum, and then the local optimizer takes over to find the minimum. (Bilchev & Parmee, 1996) developed a search space reduction methodology, which was called the Inductive Search. The problem of global optimisation is partitioned into a sequence of subproblems, which are solved by searching for partial solutions in subspaces with smaller dimensions.

This method has been used to solve the Automatic Test Pattern Generation Problem in Programmable Logic Arrays (PLAs), that is to find an effective set of input test vectors,
