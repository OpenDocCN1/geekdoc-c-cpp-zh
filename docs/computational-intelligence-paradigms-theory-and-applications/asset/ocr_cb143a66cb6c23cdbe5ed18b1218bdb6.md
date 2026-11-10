bership functions are commonly used to avoid time and space complexity.

*Fuzzy combination:* The Boolean operators such as “AND” and “OR” are used as connectives in the fuzzy rules. These operators are known as fuzzy combination operators since they are used to combine more than one antecedent part.

The fuzzy AND is expressed as

$$\mu_{A\cap B}=\min(\mu_A(x),\mu_B(x))$$

Though the fuzzy AND is similar to the Boolean AND the difference is that, the Boolean AND can perform with only 0 and 1, while the fuzzy AND performs for the numbers between 0 and 1.

The fuzzy OR is expressed as

$$\mu_{A\cup B}=\max(\mu_A(x),\mu_B(x))$$

Though the fuzzy OR is similar to the Boolean OR the difference is that, the Boolean OR can perform with only 0 and 1, while the fuzzy OR performs for the numbers between 0 and 1.

*Consequence:* Using the combination operators AND/OR the fuzzified inputs are combined and the rule strengths are determined. Then the output membership functions are clipped at the rule strength to obtain the consequence. The rule consequent is correlated with the truth value of the antecedent by cutting the consequent membership function at the level of the antecedent truth. This process is referred to as clipping or alpha cut. The top most membership function is cut, therefore some information loss occurs. In order to preserve the unique shape of the membership function scaling is preferred over clipping. In scaling the degree of the membership function of the rule consequent is multiplied by the truth value of the antecedent, thus reducing the loss of information.

*Aggregation of Outputs:* The process of unification of the outputs of all the rules is known as aggregation. The clipped or scaled membership functions are combined into a single fuzzy set. Each individual fuzzy rule yields a consequence, from which the overall output is to be computed. All the consequences are aggregated by using the “AND” or “OR” connectives. The process of aggregating the rules using “AND” connective is known as conjunctive aggregation and the process of aggregating the rules using “OR” connective is known as disjunctive aggregation.

*Defuzzification:* The final step in the Mamdani Inference method is defuzzification. In order to obtain a crisp output number several defuzzification methods can be used. The aggregated output from the previous step acts as the input to the defuzzification module and outputs a single crisp number. Though there are several defuzzification methods such as max membership principle, weighted average, centroid, center of sums,