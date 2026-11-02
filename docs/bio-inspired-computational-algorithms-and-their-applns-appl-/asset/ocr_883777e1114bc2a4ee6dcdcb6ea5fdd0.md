iii. *Natural Selection:* The chromosomes are ranked from the lowest to highest cost. Of the total of chromosomes in a given generation, only the top $N_{keep}$ are kept for mating and the rest are discarded to make room for the new offspring.

iv. *Mating:* Many different approaches have been tried for crossover in continuous GAs. In crossover, all the genes to the right of the crossover point are swapped. Variables are randomly selected in the first pair of parents to be the crossover point: $\alpha = (U(0,1)N_{var})$ , where $U(0,1)$ is the uniform distribution. The parents are given by [Randy L. Haupt & Sue Ellen Haupt, 2004]:

$parent_1 = [P_{m1},...,P_{mN_{var}}]$  
$parent_2 = [P_{d1},...,P_{dN_{var}}]$  (32)

where subscripts $m$ and $d$ represent the mom and dad parent. Then the selected variables are combined to form new variables that will appear in the children.

$pnew_1 = p_{m\alpha} + \beta[p_{d\alpha} - p_{m\alpha}]$  
$pnew_2 = p_{d\alpha} + \beta[p_{m\alpha} - p_{d\alpha}]$  (33)

where $\beta$ is a random value between 0 and 1. The final step is to complete the crossover with the rest of chromosome:

$offspring_1 = [P_{m1},P_{m2},...,pnew_1,...,P_{mN_{var}}]$  
$offspring_2 = [P_{d1},P_{d2},...,pnew_2,...,P_{mN_{var}}]$  (34)

v. *Mutation:* If care is not taken, the GA can converge too quickly into one region of the cost surface. If this area is in the region of the global minimum, there is no problem. However, some functions have many local minima. To avoid overly fast convergence, other areas of the cost surface must be explored by randomly introducing changes, or mutations, in some of the variables. Multiplying the mutation rate by the total number of variables that can be mutated in the population gives the amount of mutation. Random numbers are used to select the row and columns of the variables that are to be mutated.

vi. *Next Generation:* After all these steps, the starting population for the next generation is ranked. The bottom ranked chromosomes are discarded and replaced by offspring from the top ranked parents. Some random variables are selected for mutation from the bottom ranked chromosomes. The chromosomes are then ranked from lowest cost to highest cost. The process is iterated until a global solution is achieved [Randy L. Haupt & Sue Ellen Haupt, 2004].

# 4.2.3 Image fusion

A set of input images of a scene, captured at a different time or captured by different kinds of sensors at the same time, reveals different information about the scene. The process of extracting and combining data from a set of input images to form a new composite image with extended information content is called image fusion.