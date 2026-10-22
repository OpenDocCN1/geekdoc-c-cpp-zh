the resolution method it implements.

+   - Flexible and dynamic organization.
+   - Adequacy of the architecture to the use of learning techniques.

A key idea is that each agent is decomposed in very simple behaviours. These access the blackboard by way of some input and output variables. As two different behaviours may modify the same variable a fusion method (called behaviour blending) is provided [48]. The advantage of this method is related to scalability and learning: while in a subsumption architecture [15] the management of agents depends on the behaviours they implement [51]; with the proposed architecture the management resides on the fusion method. A fuzzy rule base carries on this fusion, enabling/disabling the output of the different behaviours, both totally and partially [48, 3, 51]. This way, the system can be trained with only some simple behaviours, and then new behaviours can be added without modifying the previous ones: only the fusion rule base needs to be re-trained. When an agent is specified, the user may supply three kinds of blocks that are placed inside the agent’s execution loop:

+   - A common block that is executed before any behaviour.
+   - Series of behaviours that are executed concurrently.
+   - A blender block that specifies how the outputs of the behaviours will be fused.

All these blocks must satisfy a constraint: the execution time of each one must be computer bound, so there must not be infinite loops. The language itself assures that this constraint holds for all the blocks, and it is a necessary requirement for getting basic real time support, although the language doesn’t support fixed time scheduling. It is the user responsibility to make the appropriate tests to obtain a certain control cycle duration. For the blending process to work each behaviour defines what global output variables are to be fused. Thus they only modify local copies of those variables during the behaviour execution. The blender applies inference over fuzzy rules, defined using some input global variables as the antecedent and some behaviour names as the consequent. Last, the equation 3.8 is applied to each blended output variable.

```
α_j = pri_j · beh_j  (3.7)

ov_i = ( Σ_j α_j · lov_ij ) / ( Σ_j α_j )  (3.8)
```

where:

+   - ov_i is the i-th global output variable,