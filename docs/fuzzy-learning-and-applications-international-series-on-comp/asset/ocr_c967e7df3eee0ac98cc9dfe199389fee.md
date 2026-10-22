in the mechanisms of natural selection and genetics. Currently, these algorithms are being highly considered above all in those problems with complex solution spaces for those which we do not have good algorithms to solve them.
Next, we describe the main characteristics of the GA:

# Representation

The number of rules is known and constant if the proposal is to tune a previous rule base with a fixed number k of rules, but it is unknown and variable (N ∈ [1..MAX]) if we want to achieve processing completely, i.e., “generating and tuning” task. Firstly, we show a possible representation of the solutions to generate and tune a rule base, and we will see how this representation can be used to tune a rule base introduced previously (“only tuning” task).

Populations in this GA are composed of individuals H_i, i = 1, …, popsize, represented as follows:

# Individual H_i :

R_1^i R_2^i … R_MAX^i  d_1^i d_2^i … d_MAX^i
Rule set          Control set

where the rule R_h^i = {Ã_h^{i1} Ã_h^{i2} … Ã_h^{ip} B̃_h^i} (1 ≤ h ≤ MAX, 1 ≤ i ≤ popsize) consists of fuzzy values for the p input variables and output variable, which are represented as:

Ã_h^{ij} = (a_{h1}^{ij}, a_{h2}^{ij}, a_{h3}^{ij}, a_{h4}^{ij}),  (1 ≤ h ≤ MAX, 1 ≤ i ≤ popsize, 1 ≤ j ≤ p)
B̃_h^i = (b_{h1}^i, b_{h2}^i, b_{h3}^i, b_{h4}^i),      (1 ≤ h ≤ MAX, 1 ≤ i ≤ popsize)

i.e., trapezoidal fuzzy numbers with a_{hl}^{ij}, b_{hl}^i ∈ R, (1 ≤ h ≤ MAX, 1 ≤ l ≤ 4, 1 ≤ i ≤ popsize, 1 ≤ j ≤ p). Values d_h^i ∈ {0,1} (1 ≤ h ≤ MAX, 1 ≤ i ≤ popsize) indicate if rule h of the individual i is active in the solution (1 = active, 0 = inactive). Thus, the number N of rules in the individual i is given by the number of values d_h^i = 1, 1 ≤ h ≤ MAX.

Note that a control set is not necessary if we want to tune a previous rule base with a fixed number k of rules.

# Initial Population

To create an initial population we take into account two criteria:

+   1. Explore available information (examples, rule bases, etc.).
+   2. Explore (randomly) solution space to obtain an appropriate diversity.