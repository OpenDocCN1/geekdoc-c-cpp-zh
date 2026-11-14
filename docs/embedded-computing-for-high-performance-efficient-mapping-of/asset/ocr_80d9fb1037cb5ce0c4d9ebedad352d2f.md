```
// Cost_init = computeCost(Sol_init); // the cost of the initial solution
CostSol = Cost_init; // for now the minimum cost if the one used by this solution
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

# **FIG. 8.3**
A simulated annealing-based exploration scheme.

execution of the algorithm, there are two important aspects to consider, namely, the cooling scheme used (the simplest one gradually reduces the temperature by a constant factor \(\alpha\): \(0 < \alpha < 1\)) and the number of iterations (being the two simplest options the use of a constant number or increasing it by a constant factor \(\beta \ge 1\) in each step). Possible values for \(\alpha\) and \(\beta\) are, respectively, 0.95 and 1.01. For each new design being considered as part of a move, there is a calculation of the cost for the new solution, obtained by actual measurements, simulations, or estimation techniques.

Despite its simplicity, SA is widely used in many domains due to its resilience in the case where the search is “trapped” in local minima (as the SA algorithm can, momentarily, consider worse designs than the best found so far) and the ability to recast many domain problems as SA search problems. In many cases, the use of the “correct” parameters allows SA to find designs close to the optimum solutions.

As an alternative to SA, and depending on the size of the design space and on the importance of finding solutions close to the optimum, DSE implementations may rely on heuristic-based algorithms or even use machine learning-based approaches. Both approaches aim at accelerating the search process by exploring a much smaller number of possible design points, using a set of predefined search directions, or even skipping the evaluation of intermediate design points.