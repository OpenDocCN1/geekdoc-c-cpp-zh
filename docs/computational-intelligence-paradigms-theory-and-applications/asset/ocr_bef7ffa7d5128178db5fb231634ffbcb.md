![](bbox=[0.169, 0.101, 0.924, 0.511])

**FIGURE 11.1:** The Basic cycle of Evolution. Clouds Represent Populations of Genotypes (genes) or Phenotypes (types). Polygons Denote Processes. Solid Pentagons Represent Processes that Filter the Pool of Individuals, While the Dashed Pentagon for Mitosis and Meiosis Indicates an Increase (in this Case, Genetic Material).

# 11.5  Flow Diagram of a Typical Evolutionary Algorithm

A population of structures is maintained in EC to evolve according to rules of selection and other operators, such as recombination and mutation. Each individual in the population receives a measure of its fitness in the environment. During selection more attention is concentrated on high fitness individuals, thus exploiting the available fitness information. The processes of recombination and mutation disturb these individuals, thereby providing general heuristics for exploration. Though simple from a life scientist’s viewpoint, these algorithms are sufficiently composite to provide robust and powerful adaptive search mechanisms. Figure 11.2