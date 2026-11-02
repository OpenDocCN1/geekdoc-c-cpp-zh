![](bbox=[0.17, 0.11, 0.86, 0.53])

Fig. 8. Fault Coverage Problem of 200 possible faults solved with three HGAs

These experiments show that the proposed MHGA seems to offer a better performance than the two other HGAs: the Inductive Genetic Algorithm and the Genetic Algorithm hybridized by Simulated Annealing. We have proved on two different examples, with different complexities, that MHGA offers the greatest value of fault coverage in Automatic Test Pattern Generation Problem in digital circuits of PLA type.

# 5.3 A Quantum Inspired GA for EHW

Quantum Inspired Genetic Algorithm (QIGA) proposed in (Popa et al., 2010) uses a single chromosome, which is represented like a string of qubits, as is described in (Han & Kim, 2002; Zhou & Sun, 2005). A quantum chromosome which contains n qubits may be represented as:

$$q = \begin{bmatrix} \alpha_1 & \alpha_2 & \dots & \alpha_n \\ \beta_1 & \beta_2 & \dots & \beta_n \end{bmatrix}^T \tag{8}$$

where each couple $\alpha_i$, $\beta_i$, for $i=1,\dots,n$, are the probability amplitudes associated with the $|0\rangle$ state and the $|1\rangle$ state such that $\alpha_i^2 + \beta_i^2 = 1$ and the values $\alpha_i^2$ and $\beta_i^2$ represent the probability of seeing a conventional gene, 0 or 1, when the qubit is measured.

A quantum chromosome can be in all the $2^n$ states at the same time, that is:

$$|q\rangle = a_0|00\dots0\rangle + a_1|00\dots1\rangle + \dots + a_{2^n-1}|11\dots1\rangle \tag{9}$$

where $a_i$ represents the quantum probability amplitude, and $a_i^2$ is the probability of seeing the $i$-th chromosome from the all $2^n$ possible classic chromosomes (Zhou & Sun, 2005).