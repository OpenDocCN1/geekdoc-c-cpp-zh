```
```pseudocode
CA-IM_Recombination
1- Get Initial Parameters:
• Pt (Probability of Recombination);
• C1 (Current Chromosome 1);        // Parents Chromosomes
• C2 (Current Chromosome 2);        // Parents Chromosomes
• S [] (Situational Knowledge);
• Sbest=best chromosome of S [];
2- Create C1' and C2' //Offsprings Chromosome Recombination )
for (int i=0; i<genotypeLength; i++)
{
  if (random< Pt)
  {
    If (random <0.5)
    {
      if (random<= 0.5)
      {
        C1'[i] = Sbest[i];
        C2'[i] = Sbest[i];
      }
      else
      {
        C1'[i] = C2[i];
        C2'[i] = Sbest[i];
      }
    }
    else
    {
      C1'[i] = C2[i];
      C2'[i] = C1[i];
    }
  }
  else
  {
    C1'[i] = C1[i];
    C2'[i] = C2[i];
  }
}
3- Return Sons (C1' and C2');
```
```

Fig. 8. Recombination pseudo-code.

# ## 4. Experimental results and discussion

To evaluate the performance of the proposed algorithm CA-IM, a comparison of various tests with Distributed Genetic Algorithms utilizing the same knapsack problems was carried out. To make a comparison two kinds of algorithms based in Distributed GAs (Aguirre et al., 2000): (i) A Distributed canonical GA (denoted as DGA), and (ii) a Distributed GA-SRM (denoted as DGA-SRM) were utilized. The SRM term means “Self-Reproduction with Mutation”, and introduces diversity by means of mutation inducing the appearance of beneficial mutations.

For the CA-IM algorithm there are two versions: CA-IM_1 and CA-IM_2. The only difference is that CA-IM_1 has a fixed rate for mutation and recombination, while CA-IM_2 has a random rate for mutation and recombination. The standard CA (CAs) is the Cultural Algorithm with single population.

# ### 4.1 DGA and DGA-SRM

The DGA works with various 0/1 multiple knapsack problems (NP hard combinatorial) which from previous efforts seem to be fairly difficult for GAs (Aguirre et al., 2000). Those algorithms were evaluated on test problems which are taken from the literature. The problem sizes range from 15 objects to 105 and from 2 to 30 knapsacks and can be found in OR-Library (Beasley, 1990). The knapsack problems are defined by: problem (n, m) where n represents the number of objects and m represents the number of knapsacks. Each knapsack