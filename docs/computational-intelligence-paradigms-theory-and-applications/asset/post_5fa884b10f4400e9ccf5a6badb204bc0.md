
Example of biologically inspired computation. Other examples of biologically inspired computation include neural networks, which is computation based on analogy to animal nervous systems, artificial life, and artificial intelligence.

During the evolutionary computation process a few populations of individuals undergo simulated evolution. While solving certain specific type of problems, these individuals generally comprise potential solutions to the problem. These solutions are presented by a kind of data structure. Selection mechanism is used by simulated evolution in order to find the best fit individuals which survive. The simulated evolution will include some variation-generating methods in which individuals can generate new individuals which are different from existing structures. Mutation and recombination (simulated mating) are two common variation-generating methods. Different evolutionary computation methods will differ in

- The data structure representation of individuals
- Variation producing mechanisms
- Parent selection methods
- Survival selection methods
- Population size

Following is a basic pseudo code for an evolutionary computation algorithm:

```
Generate an initial population in a random manner
While no stopping condition do
    Select parents based on fitness
    Produce offspring with some variants of their parents
    Select a few individuals to die based on fitness
End While
```

The fitness function of individuals is usually determined by the problem to be solved. Evolutionary computation is more commonly used in the field of optimization, when a function with several parameters is specified, and the aim is to find the parameter settings that give the largest or optimal value of the function. EC does not assure to find the optimal value of the function, EC merely attempts to find a parameter setting that gives a "large" or "near optimal" function value. Hence, ECs could be represented as "search algorithms" instead of "optimization algorithms". The function that is optimized does not need to be a mathematical function—it may be the result of a computer simulation or a real-world experiment. For example, in genetic programming, the objective can be to find a formula or computer program that accomplishes a certain task. The function that is optimized is the result of applying the formula or program (represented as parse tree) to a number of test cases.

## 11.3 Brief History of Evolutionary Computation

Several scientists and researchers proved that evolutionary computation can be used as a tool for solving optimization problems in engineering during the 1950s and 1960s. The basic idea was evolving a population of candidate solutions to a given problem, using operators inspired by genetic variation and natural selection. Many other researchers developed evolutionary algorithms for optimization and machine learning problems. History itself is an evolutionary process, not just in the sense that it changes over time but also in the more strict sense that it undergoes mutation and selection.

The selection function is performed under the process of mutation. The history of evolutionary computation is broadly related more with science fiction than a factual record. The idea to use recombination in population-based evolutionary simulations did not arise in a single major innovation but in fact was commonly, if not routinely, applied in multiple independent lines of investigation in the 1950s and 1960s. Population geneticists and evolutionary biologists considered computers to study “life-as-it-could-be” (i.e., artificial life) rather than “life-as-we-know-it”.

The idea to use Darwinian principles for automated problem solving originated in the fifties, even before computers were used on a large scale. Later in the sixties, three different interpretations of this idea were developed: Evolutionary programming introduced by Lawrence J. Fogel in the U.S.A., John Henry Holland introduced a method genetic algorithm, and Ingo Rechenberg and Hans-Paul Schwefel of Germany introduced evolution strategies. There was great development in all these areas independently until the early nineties. Since then these techniques were combined as one technology, called evolutionary computing. During this period, a fourth paradigm following the general ideas of evolutionary programming, genetic algorithm, and evolutionary strategies had emerged and it was named genetic programming. These terminologies denote the whole field by evolutionary computing and consider evolutionary programming, evolution strategies, genetic algorithms, and genetic programming as sub-areas.

## 11.4 Biological and Artificial Evolution

The basic idea behind Evolutionary Computation (EC) lies under the principles of biological evolution. A set of terminology and expressions used by the EC community is illustrated in this section.

### 11.4.1 Expressions Used in Evolutionary Computation

The basis of EC technique is very simple, Darwin’s theory of evolution, and specifically survival of the fittest. Much of the terminology is borrowed from biology. A set of chromosomes comprise a population with each chromosome representing a possible solution. Every individual chromosome is made up of a collection of genes, these genes are the variables to be optimized.

The process of evolutionary algorithm involves a sequence of operations: creating an initial population (a collection of chromosomes), evaluating this population, then evolving the population through multiple generations. At the end of each generation the fittest chromosomes, i.e., those that represent the best solution, from the population are retained and are allowed to crossover with other fit members. Crossover is performed in order to create chromosomes that are more fit than both the parents by taking the best characteristics from each of the parents. Thus over a number of generations, the fitness of the chromosome population will increase with the genes within the fittest chromosome representing the optimal solution. The entire process of EC is similar to living species, in which they evolve to match their changing environmental conditions. Table 11.1 presents a brief overview of some of the terminology adopted from biology and used in EC.

### 11.4.2 Biological Evolution Inspired by Nature

The process of evolution is the gradual development of living organisms. Living organisms evolve through the interaction of competition, selection, reproduction, and mutation processes. The evolution of a population of organisms highlights the differences between an organism’s “genotype” and “phenotype.” The phenotype is the way in which response is contained in the physiology, morphology and behavior of the organism. The genotype is the organism’s underlying genetic coding (DNA).

**TABLE 11.1: A Summary of the Basic Expressions Used within EC**

| Biological Expression | EC Implication |
|---|---|
| Chromosome | String of symbols |
| Population | A set of chromosomes |
| Deme | A local population of closely related chromosomes, a subset of the total population |
| Gene | A feature, character or detector |
| Allele | Feature value |
| Locus | A position in a chromosome |
| Genotype | Structure |
| Phenotype | A set of parameters, an alternative solution or a decoded structure |

Though the basic principles of evolution (natural selection and mutation) are understood in ample, both population genetics and phylogenetics have been radically transformed by the recent availability of large quantities of molecular data. For example, in population genetics (study of mutations in populations), more molecular variability was found in the 1960s than had been expected. Phylogenetics (study of evolutionary history of life) makes use of a variety of different kinds of data, of which DNA sequences are the most important, as well as whole-genome, metabolic, morphological, geographical, and geological data.

The basic concept of evolutionary biology shows that organisms share a common origin and have diverged through time. The details and timing of these divergences of an evolutionary history are important for both intellectual and practical reasons, and phylogenies are central to virtually all comparisons among species. The area of phylogenetics has helped to trace routes to infectious disease transmission and to identify new pathogens.

For instance, consider the problem of estimating large phylogenies, which is a central challenge in evolutionary biology. Assume that there are three species X, Y, and Z. Three possible tree structures can be formed from these three species: (X, (Y, Z)); (Y, (X, Z)); and (Z, (X, Y)). Here (X, (Y, Z)) denotes Y and Z share a common ancestor, and this in turn shares a different common ancestor with X. Even if one picks a tree in random, there is one in three chance that the tree chosen will be correct. But the number of possible trees grows very rapidly with the number of species involved. For a small phylogenetic problem involving 10 species, there are 34,459,425 possible trees. For a problem involving
