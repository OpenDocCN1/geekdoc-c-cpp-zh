# ### 4.1 Optimal design in the mechanisms synthesis

The formulation of this problem demands the definition of several aspects like the space of design, the objective function, the algorithm of optimization and the restrictions (Lugo-Gonzalez et al., 2010). In the case corresponding to the synthesis of mechanisms, it is desired to diminish the error between the desired and generated trajectories besides analyzing the changes in the response of the algorithm when modifying parameters like the probability of mutation and crossing, the number of individuals and the maximum of generations, that will be evaluated by the proposed equation (3) that has characteristics applied to the approximated evaluation of the function, that involves the addition of the penalty to the presented original version in the works of (Goldberg, 1989), which is:

$$F = \frac{1}{N} * \sqrt{\frac{\sum_{i=1}^{N}\left(C_{eu}(v)-C_{eg}(v)\right)^2 + \left(C_{iu}(v)-C_{ig}(v)\right)^2}{n}} \tag{3}$$

Applying a division of the number of individuals $ni$ in addition to a factor of division by the reciprocal of $N$, that is the number of precision points, it adds a penalty whose objective is to recover the individuals that do not fulfill the initial restrictions known as the conditions of Grasof.

In order to finalize, the optimization algorithm uses four criteria of convergence that are defined as:

+   - *reng=* Is the first restriction, this one is the first evaluation in which it is verified if the population fulfills the restrictions of Grasof (specific condition of mechanism synthesis).
+   - *maximogen=* Defines the maximum number of times that the algorithm can evaluate the objective function. An additional call to this implies the conclusion of the search without reaching a solution.
+   - *minimerror=* Defines the minimum value of error allowed in the objective function to being compared with the generated function. A change of value in the parameter of minimum error implies the conclusion of the search without reaching a solution.
+   - *condrep=* Defines the number of times that the same value can be repeated into the evaluation before proceeding to the following operation.

Being fulfilled these last conditions to the evaluation; the algorithm will stop its search having presented the optimal values that better satisfy the restrictions and conditions.

# ### 4.2 Elliptical trajectory with parameters optimization of GA, 18 precision points, and a four-bar mechanism

The obtained research results in (Cabrera et al., 2002, Laribi et al., 2004, Starosta, 2006) are taken as a basis for describing an elliptical path with a four-link mechanism. The study case was proposed for the first time by (Kunjar and Krishnamurty, 1997). The synthesis was carried out using some variants of application using genetic algorithms or combining these with tools such as fuzzy logic. In the table 1 is shown the desired precision points to be followed by the mechanism. In the figure 6 is shown the corresponding graphic.