The result of the simulation respectively the quality of the model that results after a simulation run from *T-1* to *T* depends mainly on the settings of the control parameters *p* and *q* for the definition of the assessment curve by means of equation 8. The values for the control parameters are kept constant during a simulation period (from *T-1* to *T*). The challenge for the validation of the present model was to search for the optimal settings for these control parameters for each considered period. Our aim was to achieve the best possible model quality and therefore validity for each period.

# 5.1 Genetic algorithm

To find the optimal settings for the control parameters a genetic algorithm was used. The base forms the structure of the so-called simple genetic algorithm (SGA) according to Goldberg (1989, p. 69), which was adapted for the present challenges. The initial population for the SGA are 32 individuals that consist of a randomly generated chromosome of 28 binary numbers. In these chromosomes the four control parameters for the assessment curves of equation 8 are coded (Fig. 9). For each individual, a simulation period is run with the corresponding control parameters and the corresponding model quality is calculated. This quality represents the evaluation criteria for the suitability of a control parameter setting and can therefore be used for the fitness definition of an individual.

![](bbox=[0.281, 0.44, 0.716, 0.496])

Fig. 9. Coding of the parameters in a chromosome.

After the simulation period has been run through for each of the 32 individuals and a fitness value has been assigned to each of them, a new generation of individuals is generated. The probability for the reproduction of an individual is defined by its fitness value. The fitness values are scaled in such a way that the individual with the highest value is selected with twice the probability as an individual with an average fitness. The individual with the lowest fitness has no chance of reproduction.

The crossing rate indicates the probability that the selected individuals are crossed or copied without a change into the new generation. Crossing means the mixture or recombination of two (parent) chromosomes (Fig. 10). At the present SGA we use a crossing rate of 80%.

![](bbox=[0.206, 0.711, 0.792, 0.847])

Fig. 10. Generation of child chromosomes by crossover of the parent chromosomes.