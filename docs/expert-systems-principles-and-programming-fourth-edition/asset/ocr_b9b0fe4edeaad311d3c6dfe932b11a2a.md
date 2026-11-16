However, the LS and LN shortcut also has the detrimental effect that there is no theoretical guarantee that the sum of the conditional probabilities for each hypothesis in the net will be unity. This may not matter much to the user if the goal is simply to obtain a relative ranking of all the hypotheses in the net. For example, the user interested in the porphyry copper hypothesis may well be satisfied to know that the node indicating a favorable likelihood of copper is greatest, even if it is not 1. However, the absolute probability is important also. Even though the copper hypothesis is ranked number 1, is it worth drilling if the probability of finding copper is very low, say 0.00000001?

# Rule Interactions

Another source of uncertainty is conflict resolution of uncertainty. If the knowledge engineer specifies the **explicit priority** of rules, there is a potential source of error since the priority may not be optimum or correct. Other problems with conflict resolution occur because of the **implicit priority** of rules.

Conflict resolution is part of a major source of uncertainty caused by the interactions between rules. The interaction of rules depends on conflict resolution, and the **compatibility of rules**, as shown in Figure 5.3. The compatibility of rules has uncertainty from five major causes.

One cause of uncertainty is the potential **contradiction of rules**. Rules may fire with contradictory consequences. This may happen if the antecedents are not specified properly. As a very simple example, assume two rules in the knowledge base:

+   (1) IF there is a fire THEN put water on it
+   (2) IF there is a fire THEN don't put water on it

Rule (1) is applicable for ordinary fires such as wood fires. Rule (2) is applicable for oil or grease fires. The problem is that the antecedents are not specified precisely for the type of fire. If a fact exists "there is a fire," then both rules will be executed with contradictory consequences and a resulting increase in uncertainty.

A second source of uncertainty is **subsumption of rules**. One rule is subsumed by another if a portion of its antecedent is a subset of another rule. For example, suppose there are two rules that both have the same conclusion:

# Figure 5.3 Uncertainty Associated with the Compatibilities of Rules

![](bbox=[0.117, 0.768, 0.926, 0.933])