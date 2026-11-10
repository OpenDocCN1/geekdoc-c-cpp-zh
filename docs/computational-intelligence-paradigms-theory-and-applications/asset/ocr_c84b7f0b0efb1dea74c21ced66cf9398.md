**TABLE 11.6: Single Point Crossover**

|  | Binary string |
|---|---|
| Parent 1 | 1 1 0 0 1 \| 0 1 1 |
| Parent 2 | 1 1 0 1 1 \| 1 1 1 |
| Offspring | 1 1 0 0 1 1 1 1 |

The binary string of chromosomes along the crossover point between the two parents is used to produce a new offspring as shown in Table 11.6.

Two point crossover - two crossover points are selected, from the binary string between the two crossover points the best chromosomes form the new individual as in Table 11.7.

Uniform crossover - bits are randomly copied from the first or from the second parent as shown in Table 11.8.

# Arithmetic Crossover

A crossover operator that linearly combines two parent chromosomes to produce two new offspring according to the following equations:

*Offspring1 = a × Parent1 + (1 − a) × Parent2*  
*Offspring2 = (1 − a) × Parent1 + a × Parent2*

where a is a random weighting factor (chosen before each crossover operation). Consider the following 2 parents (each consisting of 4 float genes),

**TABLE 11.7: Two Point Crossover**

|  | Binary string |
|---|---|
| Parent 1 | 1 1 \| 0 0 1 0 \| 1 1 |
| Parent 2 | 1 1 \| 0 1 1 1 \| 1 1 |
| Offspring | 1 1 0 1 1 1 1 1 |