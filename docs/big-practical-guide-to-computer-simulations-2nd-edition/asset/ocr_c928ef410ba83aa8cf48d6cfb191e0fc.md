is P({(head,head)}) = P({head})P({head}) = 0.5·0.5 = 0.25. Similarly, for the experiment where all three coordinates of an atom inside the container are measured, one can write P([x, x + Δx] × [y, y + Δy] × [z, z + Δz]) = P([x, x + Δx])P([y, y + Δy])P([z, z + Δz]) = (Δx/Lx)(Δy/Ly)(Δz/Lz) = ΔxΔyΔz/(LxLyLz).

Often one wants to calculate probabilities which are restricted to special events C among all events, hence relative or conditioned to C. For any other event A we have P(C)=P((A ∪ A^c) ∩ C)=P(A ∩ C)+P(A^c ∩ C), which means P(A∩C)/P(C) + P(A^c∩C)/P(C) = 1. Since P(A∩C) is the joint probability of an outcome in A and C and because P(C) is the probability of an outcome in C, the fraction P(A∩C)/P(C) gives the probability of an outcome A and C relative to C, i.e. the probability of event A given C, leading to the following

# Definition 8.3 The probability of A under the condition C is

P(A|C) = P(A ∩ C)/P(C). (8.5)

As we have seen, we have the natural normalization P(A|C)+P(A^c|C)=1. Rewriting Eq. (8.5) one obtains P(A|C)P(C)=P(A ∩ C). Therefore, the calculation of P(A ∩ C) can be decomposed into two parts, which are sometimes easier to obtain. By symmetry, we can also write P(C|A)P(A)=P(A ∩ C). Combining this with Eq. (8.5), one obtains the famous Bayes' rule

P(C|A) = P(A|C)P(C)/P(A). (8.6)

This means one of the conditional probabilities P(A|C) and P(C|A) can be expressed via the other, which is sometimes useful if P(A) and P(C) are known. Note that the denominator in the Bayes' rule is sometimes written as P(A)=P(A∩(C∪C^c))=P(A∩C)+P(A∩C^c)=P(A|C)P(C)+P(A|C^c)P(C^c).

If an event A is independent of the condition C, its conditional probability should be the same as the unconditional probability, i.e., P(A|C)=P(A). Using P(A∩C)=P(A|C)P(C) we get P(A∩C)=P(A)P(C), i.e., the probabilities of independent events have to be multiplied. This was used already above for random experiments, which are conducted as independent subexperiments.