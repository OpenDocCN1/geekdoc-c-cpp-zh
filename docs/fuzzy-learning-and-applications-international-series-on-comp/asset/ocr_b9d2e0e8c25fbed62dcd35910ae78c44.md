The surrounding condition which has been violated most often is chosen.

Then the two fuzzy system inputs I1 and I2 are set respectively to the coefficient of the surrounding condition previously determined and the mean of the remaining conditions. The fuzzy rules trained are evaluated and the two defuzzified outputs O1 and O2 are obtained. The coefficient of the surrounding condition assumed to be the cause of invalidity or insufficient quality takes the value O1, while the others are each multiplied by O2/T2.

If the network offers a valid solution whose quality is insufficient, i.e., higher than the Tolerance·LowerBound value, but not very far from this value, in practice it has been seen that by leaving the coefficients almost unaltered the next solution provided by the Hopfield network will be of better quality.

We therefore decided that if the surrounding condition most violated is related to quality, the percent difference between the solution and the Tolerance·LowerBound product is calculated. If the difference remains within a pre-established threshold, coefficient modification will only involve the HC found, leaving the others unaltered. According to the algorithm outlined above, this was obtained by not multiplying each coefficient by O2/T2.

If the surrounding condition most violated is related to quality and the percent difference between the solution and the Tolerance·LowerBound product exceeds the pre-established threshold, the coefficients are all modified in the attempt to force the network to provide better solutions.

Let E be the value of the energy function calculated in correspondence of the neural solution. In order to realize the HC modification when the solution is valid but not good, a new membership function, μNotGood(E), again is considered. The degree of goodness of E is specified by the clause:

(E IS NotGood)

The membership function μNotGood (see Fig. 8.8) is characterized by only two parameters te and Me, where Me ≥ te. If E is greater than the value of Me, then the truth value is unitary. This value leads in our algorithm to the modification of all coefficients in the attempt to force the network to provide better solutions. On the other side, if the value E is in the range ]te,Me[, the membership function degree will be less than 1. According to our algorithm, this value leads to a smooth modification of the HC parameter linked to the quality of solution, leaving the others unchanged.

# 8.4.2 Membership Function Tuning

Two membership function classes were presented in the previous section, one used in order to directly compare the values of Cause(c) obtained for each surrounding condition and the other to realize the HC modification when the solution is valid but not good. Both the membership function classes play an