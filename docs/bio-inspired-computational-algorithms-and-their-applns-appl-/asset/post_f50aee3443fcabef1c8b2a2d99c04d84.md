
## Part 1

### Recent Development of Genetic Algorithm

are corrected up to several significant digits according to the number of zooms and the zooming rate. The SZGA can predict the possibility that the solution found is the exact optimum solution. The zooming factor, number of sub-iteration populations, number of zooms, and dimensions of a given problem affect the possibility and accuracy of the solution. In this chapter, we examine these parameters and propose a method for selecting the optimal values of parameters in SZGA.

## 2. The Successive Zooming Genetic Algorithm

This section briefly introduces the successive zooming genetic algorithm⁶ and provides the basis for the selection of the parameters used. The algorithm has been applied successively to many optimization problems. The successive zooming genetic algorithm involves the successive reduction of the search space around the candidate optimum point. Although this method can also be applied to a general Genetic Algorithm (GA), in the current study it is applied to the Micro-Genetic Algorithm (MGA). The working procedure of the SZGA is as follows. First, the initial solution population is generated and the MGA is applied. Thereafter, for every 100 generations, the elitist point with the best fitness is identified. Next, the search domain is reduced to (X_OPT-d^k/2, X_OPT+d^k/2), and then the optimization procedure is continued on the reduced domain (Fig. 1). This reduction of the search domain increases the resolution of the solution, and the procedure is repeated until a satisfactory solution is identified.

![](img/b6b7f8aebd1f88cc16a4011cc646fc4d_15_0.png)

Fig. 1. Flowchart of SZGA and schematics of successive zooming algorithm

The SZGA can assess the reliability of the obtained optimal solution by the reliability equation expressed with three parameters and the dimension of the solution N_VAR.

R_SZGA = [1 - (1 - (α / 2))^{...} × β_AVG]^{...} (1)

where,
α: zooming factor, β: improvement factor
N_VAR: dimension of the solution, N_ZOOM: number of zooms
N_SIF: number of sub-iterations, N_POP: number of populations
N_SF: total number of individuals during the sub-iterations (N_SF=N_SUB×N_POP)

Three parameters control the performance of the SZGA: the zooming factor α, number of zooming operations N_ZOOM, and sub-iteration population number N_SF. According to previous research, the optimal parameters for SZGA, such as the zooming factor, number of zooming operations, and sub-iteration population number, are closely related to the number of variables used in the optimization problem.

### 2.1 Selection of parameters in the SZGA

The zooming factor α, number of sub-iteration population N_SF, and number of zooms N_ZOOM of SZGA greatly affect the possibility of finding an optimal solution and the accuracy of the found solution. These parameters have been selected empirically or by the trial and error method. The values assigned to these parameters determine the reliability and accuracy of the solution. Improper values of parameters might result in the loss of the global optimum, or may necessitate a further search because of the low accuracy of the optimum solution found based on these improper values. We shall optimize the SZGA itself by investigating the relation among these parameters and by finding the optimal values of these parameters. A standard way of selecting the values of these parameters in SZGA, considering the dimension of the solution, will be provided.

The SZGA is optimized using the zooming factor α, number of sub-iteration population N_SF, and the number of zooms N_ZOOM, for the target reliability of 99.9999% and target accuracy of 10^6. The objective of the current optimization is to minimize the computation load while meeting the target reliability and target accuracy. Instead of using empirical values for the parameters, we suggest a standard way of finding the optimal values of these parameters for the objective function, by using any optimization technique, to find the optimal values of these parameters which optimize the SZGA itself. Thus, before trying to solve any given optimization problem using SZGA, we shall optimize the SZGA itself first to find the optimal values of its parameters, and then solve the original optimization problem to find the optimal solution by using these parameters.

After analyzing the relation among the parameters, we shall formulate the problem for the optimization of SZGA itself. The solution vector is comprised of the zooming factor α, the number of sub-iteration population N_SF, and the number of zooms N_ZOOM. The objective function is composed of the difference of the actual reliability to the target reliability, difference of the actual accuracy to the target accuracy, difference of the actual N_SF to the proposed N_SF, and the number of total population generated as well.

F(α, N_SF, N_ZOOM) = ΔR_SZGA + ΔA + ΔN_SF + (N_SF × N_ZOOM) (2)

where,
ΔR_SZGA : difference to the target reliability
- ΔA : difference to the target accuracy
- Δ N_SP : difference to the proposed N_SP

The problem for optimization of SZGA itself can be formulated by using this objective function as follows:

Minimize F(X) (3)

where,

X = {α, N_SP, N_ZOOM}^T
0 < α < 1
N_SP > 100
N_ZOOM > 1

The difference of the actual reliability to the target reliability is the difference between R_SZGA and 99.9999%, where reliability R_SZGA is rewritten with an average improvement factor as

R_SZGA = [1 − (1 − (α / 2)^N_ZOOM × β_AVG^N_SP)^(N_ZOOM − 1)] (4)

Here, we can see the average improvement factor β_AVG, which is to be regressed later on. The difference of realized accuracy to the target accuracy is the difference between accuracy A and 10^4, where accuracy A is actually the upper limit and may be written as,

A = α^(N_ZOOM − 1) (5)

The difference of the actual N_SP to the proposed N_SP is difference between N_SP and 100^7 . In organizing the optimization algorithm, each element in the objective function is given different weights according to its importance. Thus, the target reliability and target accuracy are met first, and then the number of total population generated is minimized. Although any optimization technique could have been used to solve eq.(3), one can adopt the SZGA in optimizing the SZGA itself to obtain a solution fast and accurately.

The parameters in SZGA have been optimized by using the objective function and improvement factor averaged after regression for a test function ^9. The target reliability is 99.9999% and target accuracy of solution is 10^4. The proposed number of sub-iteration population N_SP is 100. Table 1 shows the optimized values for the SZGA parameters for four cases of different number of design variables.

We found a similar tendency to Table 1 for test functions of various numbers of design variables. We also found that the recommended number of sub-iteration population N_SP would no longer be acceptable to assure reliability and accuracy for the cases whose number of design variables is over 1. A much greater number of sub-iteration population is needed to obtain an optimal solution with the proper reliability (99.9999%) and accuracy (10^4).

To confirm our optimized result, we fixed two parameters in the feasible domain that satisfy the target reliability and target accuracy, and checked the change in the objective function as a function of the remaining parameter. Examples of the change in the objective function for the case of four design variables showed the validity of the obtained optimal values of the
parameters. Although these values may not be valid for all the other cases, they can be used as a good reference for new problems. Some other ways of choosing the values of these parameters will be given later on.

Table 1. Result of optimized parameters in SZGA for different number of design variables

| No. of Variables | 2 | 4 | 8 | 16 |
|---|---|---|---|---|
| Zooming Factor α | .02573 | .1303 | .4216 | .5176 |
| Nzoom | 5 | 8 | 17 | 22 |
| Nsp | 1,000 | 2,000 | 9,510 | 1,479,230 |
| No. of Function Evaluation | 5,000 | 16,000 | 161,670 | 32,543,060 |

### 2.2 Programming for successive zooming and pre-zoning algorithms

Programming the SZGA is simple, as explained below. This zooming philosophy may not be confined only in GA, but can be applied to most other global search algorithms. Let Y(i) be the global variables ranging YMIN(i) ~ YMAX(i), where i is the design variable number. Z(i) consists of local normalized variables ranging 0-1. Thus, the relation between them is as follows in FORTRAN;

```
DO 10 I=1,NVAR
10 Y(I)=YMIN(I)+(YMAX(I)-YMIN(I))*Z(I)
```

The relation between local variable Z(I) and local variable X(I) (0~1) in the zoomed region is as follows;

```
DO 12 I=1,NVAR
12 Z(I)=ZOPT(I,JWIN-1)+ALP**(JWIN-1)*(X(I)-0.5)
```

Where, ZOPT(I,JWIN) is the elitist in the zoom step (JWIN-1), and ALP is the zooming factor. Note that ZOPT(I,JWIN-1) is more logical. However, the argument is increased by one to meet old versions of FORTRAN, which require a positive integer as a dimension argument. Based on the elitist in step (JWIN-1), we are seeking variables in step JWIN. Please note that ZOPT(I,1)=0.

A pre-zoning algorithm adjusts the guessed initial zone to a very reasonable zone after one set of generation.

```
DO 14 I=1,NVAR
    YMIN(I)=YINP(I)-BTA*ABS(YINP(I))
14  YMAX(I)=YINP(I)+BTA*ABS(YINP(I))
```

Where, YINP(I) is the elitist obtained after one set of generation. Thus, we eliminate the assumed initial boundary, and establish a new reasonable boundary. The coefficient BTA may be properly selected, say 0.5.
