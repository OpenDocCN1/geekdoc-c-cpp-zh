least square error (LSE) ||W* Y* − Yd||² and is given by:

Y* = (W*ᵀ W*)⁻¹ W*ᵀ Yd  (2.19)

which can be computed in a recursive way [42][5].

The previous algorithm is a batch procedure, where the parameters (singletons) are updated from the whole training set. A simpler alternative is the incremental LMS rule, where the parameters are updated every time an input-output pair is presented [41],

y*i_new = y*i_old + μ[y_d(x)−y(x)] w*i(x)    i = 1, ... N  (2.20)

where μ is a constant. It is interesting to note that (2.20) is also obtained from a gradient rule [43]. Note that the membership grade of input x to the fuzzy set whose singleton is being updated is taken into account by weighting the increment by w*i(x). The closer the input is to the fuzzy set core, the larger the value of w*i(x); thus the singleton is tuned depending on its influence on the output. Another way to consider such dependence consists in updating only the singleton whose associated rule antecedent is maximum, thus:

y*i_new = y*i_old + μ(y_d(x)−y(x))  (2.21)

where i is the index of the rule so that w*i(x) = = max[w*1(x), w*2(x), ... w*N(x)]. This is certainly the outstar incremental rule, which is employed to train the Grossberg layer in the counterpropagation network. The latter is intended to be used for clustering purposes, but can also approximate functions [44]. The principle is just the same as in the general architecture in Fig.2.17, but in this network the sets in the first layer (Kohonen's layer) are crisp instead of fuzzy. The simplicity of the rule in (2.21) makes it a good candidate for silicon implementation; thus we have chosen it to demonstrate its viability.

The parameter μ in (2.21) determines the learning speed. Since we will have a minimum increment Δy*i_min = (y*i_new−y*i_old)_min for the updated singleton value due to the limited resolution, this constant must be selected to fulfill: