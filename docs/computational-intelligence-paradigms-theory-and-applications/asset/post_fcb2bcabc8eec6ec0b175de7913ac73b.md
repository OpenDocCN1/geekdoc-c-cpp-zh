
![](img/d9a4cc12c48f7466f309cbd3c4549c73_714_0.png)

**FIGURE 15.4:** Plot of Distance and Optimum Length

### 15.10.4 Illustration 4: Ant Algorithm for the Quadratic Assignment Problem (QAP)

The following MATLAB code implements the QAP to assign n departments to n unique locations.

```matlab
clc;
clear;

% THE DISTANCE/FLOW MATRIX
% UPPER HALF = DISTANCE, LOWER HALF = FLOW
DF = [NaN 1 2 3 4 4;
      5 NaN 1 2 2 1 2 3;
      2 3 NaN 1 2 2 1 2;
      4 0 0 NaN 4 3 2 1;
      1 2 0 5 NaN 1 2 3;
      0 2 2 2 10 NaN 1 2;
      0 2 0 2 0 5 NaN 1;
      6 0 5 10 0 1 10 NaN];

% PROBLEM SIZE...(NUMBER OF SITES OR DEPTS)
pr_size = size(DF, 1);
ants = 5; % NUMBER OF ANTS
max_assigns = 100000; % NUMBER OF ASSIGNMENTS
% (WHEN TO STOP)
optimal = 107; % OPTIMAL SOLUTION
a = 1; % WEIGHT OF PHEROMONE
b = 5; % WEIGHT OF HEURISTIC INFO
lamda = 0.8; % EVAPORATION PARAMETER
Q = 10; % CONSTANT FOR PHEROMONE UPDATING
AM = ones(ants,pr_size); % ASSIGNMENTS OF EACH ANT
min_cost = -1;

% HEURISTIC INFO - SUM OF DISTANCES BETWEEN SITES
for i=1:pr_size
    D(i) =sum( DF(i:i-1,i))+sum(DF(i,i+1:pr_size));

end

% START THE ALGORITHM
assign = 1;
while (assign <= max_assigns) & ( ( min_cost > optimal) | (min_cost == -1) )
    % ============ FIND PHEROMONE =============

    % AT FIRST LOOP, INITIALIZE PHEROMONE
    if assign==1
        % SET 1 AS INITIAL PHEROMONE
        pher = ones(8);

    % IN THE REST OF LOOPS, COMPUTE PHEROMONE
    else
        for i=1:pr_size
            for j=1:pr_size
                tmp = zeros(ants,pr_size);
                tmp( find(AM==j)) = 1;
                tmp = tmp(:,i);
                tmp = tmp .* costs';
                tmp( find(tmp==0) ) = [];
                tmp = Q ./ tmp;
                delta(i,j) = sum(tmp);
            end
        end
        pher = lamda * pher + delta;
    end
    % ============= ASSIGN DEPTS TO SITES =============

    % EACH ANT MAKES ASSIGNMENTS
    for ant=1:ants
        % GET RANDOM DEPT ORDER
        depts = rand(pr_size, 2);
        for i=1:pr_size
            depts(i,1) = i;
        end
        depts = sortrows(depts,2);

        % KEEP AVAILABLE SITES IN A VECTOR
        for i=1:pr_size
            free_sites(i) = i;
        end
        pref = ones(pr_size,1); % PREFERENCE FOR EACH SITE
        prob=ones(pr_size,1);% PROBABILITIES FOR EACH DEPT
        for dept_index=1:pr_size
            % GET SUM OF THE PREFERENCES
            % AND THE PREFERENCE FOR EACH SITE
            pref_sum = 0;
            for site_index=1:size(free_sites,2)
                tmp_pher=pher(depts(dept_index),free_sites(site_index));
                pref(site_index) = tmp_pher^a * (1/D(free_sites(site_index)))^b;
                pref_sum = pref_sum + pref(site_index);
            end

            % GET PROBABILITIES OF ASSIGNING THE DEPT
            % TO EACH FREE SITE
            prob = free_sites';
            prob(:,2) = pref / pref_sum;

            % GET THE SITE WHERE THE DEPT WILL BE ASSIGNED
            prob = sortrows(prob,2);
            AM(ant,dept_index) = prob(1);

            % ELIMINATE THE SELECTED SITE FROM THE
            % FREE SITES
            index = find(free_sites==prob(1));
            prob(1,:) = [];
            free_sites(index) = [];
            pref(index) = [];
        end

        % GET THE COST OF THE ANT'S ASSIGNMENT
        costs(ant) = 0;
        for i=1:pr_size
            for j=1:i-1
                dept_flow = DF(i,j);
                site1 = AM(ant,i);
                site2 = AM(ant,j);
                if site1 < site2
                    sites_distance = DF(site1, site2);
                else
                    sites_distance = DF(site2, site1);
                end
                costs(ant) = costs(ant) + dept_flow * sites_distance;
            end
        end
        if (costs(ant) < min_cost)|(min_cost==-1)
            min_cost = costs(ant);
            ch_assign = AM(ant,:);
        end
    end
    if mod(assign,100) == 0
        disp(sprintf('Assignments so far : %d\nCheapest cost : %d', assign, min_cost));
    end
    assign = assign + 1;
end

disp(sprintf('Cheapest Cost : %d', min_cost));
disp(sprintf('Assignments : %d', assign-1));
disp(' ');
disp('Assignment');
disp('----------');
ant_index = find(costs==min(costs));
for i=1:pr_size
    disp(sprintf('Dept %d to Site %d', i, ch_assign(i)));
end
```

**Output:** Cheapest Cost : 107  
Assignments : 4945

Assignment

- Dept 1 to Site 2
- Dept 2 to Site 1
- Dept 3 to Site 5
- Dept 4 to Site 3
- Dept 5 to Site 4
- Dept 6 to Site 8
- Dept 7 to Site 7
- Dept 8 to Site 6

## Summary

This chapter introduced the theoretical foundations of swarm intelligence with a focus on the implementation and illustration of particle swarm optimization and ant colony optimization algorithms. We provided a few applications on Particle optimization problems and ant colony optimization for easy understanding of the optimization problems. A set of MATLAB programs were also given for implementation of PSO and ACO. Results were analyzed, discussed, and their potentials were illustrated.

## Review Questions

- 1. Define swarm and swarm behavior.
- 2. Explain briefly on boid.
- 3. What are swarm robots?
- 4. Write a note on stability analysis of swarms.
- 5. Define Swarm Intelligence.
- 6. Explain the taxonomy of Swarm Intelligence.
- 7. Mention a few properties of swarm intelligence.
- 8. Explain briefly the applications of swarm intelligence.
- 9. Mention the usage of Particle Swarm Optimization and Ant Colony Optimization.
- 10. Represent PSO in a canonical form.
- 11. Write the algorithm of PSO and explain the operational steps briefly.
- 12. Mention a few neighborhood topologies that influence the performance of PSO.
- 13. Compare PSO with a few global optimization techniques.
- 14. State the functions used to test the performance of PSO.
- 15. Write short notes on Fuzzy PSO and Binary PSO.
- 16. Explain the Job Scheduling application using PSO.
- 17. Write a note on PSO for data mining.
- 18. Write the algorithm of ACO and explain the operational steps briefly.
- 19. How is the traveling salesman problem optimized using ACO?
- 20. What do you mean by Quadratic assignment problems?
- 21. Write a note on ACO used in data mining.
- 22. Write a MATLAB program to implement the PSO algorithm and analyze its performance on Job shop scheduling problem.
- 23. Optimize the path of a Traveling Salesman Problem using PSO algorithm in MATLAB. Compare the results with ACO.
- 24. Find the minimum of a function using Hybrid PSO in MATLAB.
- 25. Write a MATLAB program using PSO to train a feed forward neural network. Assume that the Neural network is approximating a noisy sine function.
- 26. Implement the Quadratic Assignment Problem in MATLAB using PSO and compare the results with QAP using ACO algorithm.

**Aggregation:** The combination of the consequents of each rule in a Mamdani fuzzy inference system in preparation for defuzzification.

**Algorithm:** A detailed and unambiguous sequence of instructions that describes how a computation is to proceed and can be implemented as a program.

**Allele:** Alternative form of a gene; one of the different forms of a gene that can exist at a single locus.

**Allele Loss:** Allele loss is the natural loss of traits in the gene pool over the generations of a run. Another term for allele loss is convergence. Severe allele loss results in a population incapable of solving the problem with the available gene pool.

**Ant Colony Optimization (ACO):** Heuristic search algorithm for NP-hard optimization, inspired by the foraging behavior of real ant colonies, experimentally showed that the foraging behavior can give rise to the emergence of shortest path when employed by a colony of ants

**Antecedent:** A conditional statement in the IF part of a rule, also referred to as Premise.

**Ants:** Ants are social, colony-building insects who live in self-organized groups. Their perceptive spectrum is limited to various smells and a good sense of feel. The individual ants themselves are not capable of complex thinking. There are also no superants who delegate knowledge. The special role of the queen is limited to laying eggs. Why do ant colonies act complexly and intelligently as a whole then? “Single ants aren’t smart. Ant colonies are.” This effect is called “swarm intelligence”: individuals follow simple rules to which complex behavior adds up. For example: there are two routes from the colony to food, a long one and a short one. None of the ants know which way is better and why, they choose the route by chance at first. The ants who choose the shorter route, however, walk back and forth between the colony and the food more often in the same period of time and thus leave more pheromone traces on the shorter path. This scent message signals to the other ants that this is the optimum route.

**Approximate Reasoning:** Reasoning that does not require a precise matching between the IF part of a production rule with the data in the database.

**Artificial Neural Network (ANN):** An information-processing paradigm inspired by the structure and functions of the human brain. An ANN
