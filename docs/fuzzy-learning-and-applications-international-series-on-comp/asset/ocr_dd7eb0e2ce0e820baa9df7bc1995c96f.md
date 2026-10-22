TLL = TLL - 1). If J_b > J_c, let A_b = A_0 and J_b = J_c. If k > ITMAX, stop (A_b is the best solution found and J_b is the corresponding best objective function value); otherwise, let k = k + 1 and go to step s2.

Different alternatives exist to generate the trial solutions, for example, to move the centroids over the space and then to calculate the new memberships matrix. For each centroid, if a random number is greater than P, the move is performed.

# 3.4.3 Rule Generation Agents

In order to approximate the function φ : X^p → Y that model the system, we assume the existence of a collection of data samples of the system behavior in the product space (X^p × Y), Ω = ((x_t1, x_t2, ..., x_tp), y_t) t = 1,2,...,n, where X_1, X_2,..., X_p are the domains of discourse of the inputs and Y is the domain of the output.

We consider that we have a collection of k_1 fuzzy sets in the input space X^p and a collection of k_2 fuzzy sets in the output space Y (collections obtained because we have done a fuzzy clustering in each of these domains, or because we have an a priori information about a fuzzy partition of these domains). In this way we have a collection of possible k_1 * k_2 fuzzy rules of the form:

R_h: If x is A^i then y is B^j [w_ij]
i = 1,...,k_1 j = 1,...,k_2 (3.4)

where x = (x_1,...,x_p) and A^i could be a fuzzy set obtained using a fuzzy clustering of X^p, or obtained as A^i = (A_1^i * ... * A_p^i) with * a T-norm.

In order to infer with the collection of fuzzy rules we have decided, because of its simplicity, to use as the approximate reasoning method the Mizumoto Simplified Method [45], where the fuzzy sets of the consequent are substituted by a singleton value, i.e., real numbers. As far as fuzzy control is concerned, it is well known that we can use fuzzy rules with singletons in the consequents without losing the performance of the control. This value can be obtained using the center of gravity defuzzification method over B_h:

v_h = ∫ B_h(y) y ∂y / ∫ B_h(y) ∂y

So we can rewrite(3.4) as:

R_h : If x is A^i then y is v_j, h = 1,...,k

where v_j is the singleton consequent associated to each fuzzy rule.

With the given I/O pairs (x_t, y_t), where x_t ∈ X^p, y_t ∈ Y, and t = 1,2,...,n, a fuzzy clustering is performed in the input-output product space (X^p × Y),