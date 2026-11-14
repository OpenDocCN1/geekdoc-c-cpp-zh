
In this context, the decision maker must provide a set of weights \( w_i > 0 \) to each objective function \( f_i(x) \) according to their importance:

```
\(\min_{x \in X} \sum_{i=1}^k w_i f_i(x), \quad s.t. \ x \in X\)
```

This approach requires normalizing the objective functions since they express incomparable metric values, e.g., execution time and power dissipation. Furthermore, this method cannot identify Pareto points if they are in the nonconvex regions of the Pareto frontier.

- \(\epsilon\)-constraint method. Instead of weights, this method requires selecting one objective function \( f_i(x) \) to be minimized, while the remaining objective functions are constrained by an upper-bound limit \( \epsilon_i \):

```
\(\min f(x) \\
s.t. \quad x \in X, f_i(x) \le \epsilon_i, \quad \text{for } i \in \{1, ..., k\} \setminus \{j\}\)
```

- Utility function method. This is a general method that requires a utility function \( u(t) \) expressing preferences between designs. If \( u(f_1(x), ..., f_k(x)) > u(f_1(y), ..., f_k(y)) \), then design \( x \) is preferable over \( y \) allowing the best design to be determined by solving:

```
\(\max \ uf(x), \quad s.t. \ x \in X\)
```

In practice, finding the population of all feasible designs is a computationally intensive process as the number of possible sequences of optimizations used to generate each individual design is extremely large. Therefore, developers rely on metaheuristic optimization algorithms, such as simulated annealing or evolutionary algorithms [3], to guide the search process. Alternatively, developers can combine the methods described earlier to rank designs and/or identify their neighbors, and find (possibly in an iterative fashion) feasible designs close to the Pareto optimal solutions.

## 8.2.3 DSE AUTOMATION

The automation of the DSE process is based on three major components: the search space algorithm, the definition (or synthesis) of each design point being explored, and the evaluation of each design point. For each of these components, the DSE process can use several techniques, namely:

- Search space algorithm approaches include: 1—combinatorial optimizations, such as Simulated Annealing (SA), Tabu-Search (TS), Genetic Algorithms (GA), Ant Colony optimization algorithms (ACO), Particle Swarm Optimization (PSO); 2—Integer-Linear Programming (ILP) solvers;
- 3—heuristic-based and domain- or problem-specific search algorithm;
- 4—general search algorithms such as dynamic programming and branch and bound;
- Definition of each design point may involve the use of specific (sequences of) source code transformations (see Chapter 5), as well as assigning specific values to application variables or even substituting a specific function/algorithm with an equivalent and potentially more efficient variant. The automation of the DSE process is thus predicated on the automation of the actions required to “construct” or define each design point. While there are tools, such as compilers, offering interfaces that allow an external DSE process to control its operation (e.g., via the automated insertion of compiler directives to control the sequence of transformations—see Chapter 6), in other cases this automation is not supported and requires developer intervention. For example, developers may not use source-level directive-driven programming models (e.g., OpenMP—see Chapter 6).
- Design point evaluation can be performed by deploying and running the design on the target computing system, or alternatively using simulators and estimators, to produce cost metrics such as execution time, energy, and power consumption. Estimating the cost of a design often involves analyzing the compiler generated IR (Intermediate Representation) or the corresponding assembly code (when targeting computing engines with an ISA as is the case of microprocessors). Depending on the objectives of the DSE, this evaluation can be simplified, for instance, when searching for the minimum program size. In this case, the evaluation simply needs to inspect the size (in bytes) of the code generated for the function/program being optimized.

One of the most popular methods for exploring design spaces is simulated annealing (SA) [1]. SA is a probabilistic iterative method proposed for solving combinatorial optimization problems based on an analogy with the thermodynamics concepts of cooling and heating. The algorithm relies on the abstract notion of temperature (and thus vibration of molecules), where at high temperatures it explores design points in the space “distant” from the current best design points. At higher temperatures, the reach of the search (or move) is thus more “global.” The algorithm then cools-off narrowing its search reach, confining the search to more “local” designs next to the best design solutions found so far. The algorithm engages in a series of these heating and cooling cycles (or iterations), at each lowering the amplitude of the “temperature swing,” until it reaches a stable state where it has identified the best solution or solutions.

Fig. 8.3 presents an example of an SA-based algorithm. The initial temperature (T0) and the number of iterations (iter) are important parameters of this algorithm. Usually, these parameters are calculated based on search space characteristics. During the execution of the algorithm, there are two important aspects to consider, namely, the cooling scheme used (the simplest one gradually reduces the temperature by a constant factor \(\alpha\): \(0 < \alpha < 1\)) and the number of iterations (being the two simplest options the use of a constant number or increasing it by a constant factor \(\beta \ge 1\) in each step). Possible values for \(\alpha\) and \(\beta\) are, respectively, 0.95 and 1.01. For each new design being considered as part of a move, there is a calculation of the cost for the new solution, obtained by actual measurements, simulations, or estimation techniques.

2Assuming, in this case, that the optimizations applied preserve the functionality of the program. However, this is not always the case, thus requiring functional verification by executing or simulating the transformed program.

### FIG. 8.3
A simulated annealing-based exploration scheme.

```
// Cost_init = computeCost(Sol_init); // the cost of the initial solution
CostSol = Cost_init; // for now the minimum cost is the one used by this solution
T_min = 0; // the minimum temperature considered (e.g., a value near zero
temp = T_0; // the initial temperature
alpha = 0.95; // the constant factor used to decrease the temperature
iter = 1; // the number of iterations
beta = 1.0; // the factor used to decrease the number of iterations
do { // iterate for the number of temperatures requested
    for(int i = 0; i<iter; i++) { // iterate for the prescribed number of moves
        Sol_new = Move();
        CostNew = computeCost(Sol_new); // compute the cost of tentative best design
        delta = CostNew - CostSol;
        if (delta > 0) { // if the tentative design is worse...
            if (rand() > exp(-1*delta/temp)) { // still considers the move
                CostSol = CostNew; // update the current cost
            }
        } else { // update the minimum
            if(CostNew < CostMin) {
                CostMin = CostNew;
                UpdateBest(Sol_new);
            }
            CostSol = CostNew; // update the current cost
        }
    }
    temp = alpha * temp; // decrease the temperature.
    iter = beta * iter; // Increase the iterations.
} while(temp > T_min); // if temp is zero or approximately zero the search finishes
```

Despite its simplicity, SA is widely used in many domains due to its resilience in the case where the search is “trapped” in local minima (as the SA algorithm can, momentarily, consider worse designs than the best found so far) and the ability to recast many domain problems as SA search problems. In many cases, the use of the “correct” parameters allows SA to find designs close to the optimum solutions.

As an alternative to SA, and depending on the size of the design space and on the importance of finding solutions close to the optimum, DSE implementations may rely on heuristic-based algorithms or even use machine learning-based approaches. Both approaches aim at accelerating the search process by exploring a much smaller number of possible design points, using a set of predefined search directions, or even skipping the evaluation of intermediate design points.
