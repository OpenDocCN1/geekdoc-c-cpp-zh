which are able to cover as many as possible faults in the circuit (we have taken into account two PLA structures with a total number of 50 and respective 200 stuck-at 0 possible faults).

(Wong & Wong, 1994) designed a HGA using the algorithm of Simulated Annealing as local optimizer. The optimisation process in Simulated Annealing is essentially a simulation of the annealing process of a molten particle. Starting from a high temperature, a molten particle is cooled slowly. As the temperature reduces, the energy level of the particle also reduces. When the temperature is sufficiently low, the molten particle becomes solidified. Analogous to the temperature level in the physical annealing process is the iteration number in Simulated Annealing. In each iteration, a candidate solution is generated. If this solution is a better one, it will be accepted and used to generate yet another candidate solution. If it is a deteriorated solution, the solution will be accepted with some probability.

Each of this two methods of hybridisation discussed above have some advantages. The inductive search effort at each inductive step controls the trade-off between the

```
    Procedure MHGA
    begin
        Initialize a partial solution for N = 1 and establish the initial temperature T_0;
        for k = 2 to N_p,
            Generate randomly the initial population of chromosomes;
            repeat
                append each chromosome to the partial solution, and evaluate it;
                repeat
                    select, proportional with fitness, 2 parents;
                    apply crossover to obtain 2 offsprings;
                    apply mutation to the new chromosomes;
                    calculate the fitness of new chromosomes;
                    the new chromosomes are accepted or not accepted;
                until  end of the number of chromosomes
                update the population, according with the fitness;
                the temperature is decreased;
            until end of the number of generations
            Update the partial solution;
        end
    end
```

Fig. 6. The structure of the MHGA

computational complexity and the expected quality of results, while Simulated Annealing avoids the premature convergence and reduces the adverse effects of the mutation operation. In (Popa et al., 2002) we proposed a HGA that cumulates all these advantages in a single algorithm, through a double hybridisation of the Genetic Algorithm: with Inductive Search on the one hand, and with Simulated Annealing technique on the other hand. The structure of the Multiple Hybridated Genetic Algorithm is presented in figure 6.

We have conducted the experiments with all three HGAs described above, in the purpose to find the maximum fault coverage with a limited number of test vectors. We have tested first a PLA structure with 50 potential "stuck-at 0" faults, taking into account the maximum