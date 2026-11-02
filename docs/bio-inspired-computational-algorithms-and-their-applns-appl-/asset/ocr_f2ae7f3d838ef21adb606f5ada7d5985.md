# 3.1 Mutation and recombination

In mutation operation the cultural knowledge (such as situational knowledge) as well as the standard binary mutation operation (known as “bit-flip mutation”) is utilized. If the cultural knowledge is utilized during the mutation process, the mutated chromosome genes are replaced by the best genes from chromosome stored in situational knowledge with P_M probability, otherwise, the genes are inverted by bit-flip mutation. The chromosome chosen among a set of chromosomes from situational knowledge can be the best chromosome or a random chromosome.

The bit-flip mutation is a common operation applied in evolutionary algorithms to solve a problem with binary representation. Consequently, each bit from current mutated chromosome is flipped, i.e. the value of the chosen gene is inverted also with probability of mutation P_M. Figure 7 shows the pseudo-code of mutation utilized by CA-IM.

```
```
CA-IM Mutation
1- Get Initial Parameters:
• P_M (Probability of Mutation);        • C (Current Chromosome) ;
• S [] (Situational Knowledge);        • Sbest (best chromosome of S []);
• Srandom= random chromosome of S [];
2- Create C' (Chromosome Mutation)
If (random <=0.5)
{
    for (int i=0; i< genotypeLength; i++)
    {
        if (random <=P_M)
        {
            if (random <=0.5)
                C'[i]=Sbest[i];
            else
                C'[i]=Srandom[i];
        }
    }
}
else
{
    for (int i=0; i< genotypeLength; i++)
    {
        If (random <=P_M)
            C'= flip(C, i);
    }
}
3- Return C';
```
```

Fig. 7. Mutation pseudo-code.

In recombination operation the cultural knowledge as well as the standard binary recombination operation (known as “uniform recombination”) is also utilized. In the uniform recombination the bits are randomly copied from the first or from the second parent to the genes in the offspring chromosomes, in any sequence of ones and zeros. Figure 8 shows the pseudo-code of CA-IM recombination.

If the cultural knowledge is utilized during the recombination process, the chromosome genes are replaced by the best genes from chromosome stored in situational knowledge with P_R probability. Otherwise, the genes are replaced with genes from their parents. Here only the best chromosome is chosen from situational knowledge during the recombination process.