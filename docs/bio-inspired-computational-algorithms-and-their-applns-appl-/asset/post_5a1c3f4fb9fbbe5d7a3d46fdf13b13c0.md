
In Equation 2, c_i represents the subjective value of the i-th project. Equations 1 and 2 are formally equivalent. However, the resulting value of V only makes sense if there is a process to assign meaningful values to c_i.

Before we proceed to the description of the rest of the assumptions, we need to introduce the concept of elementary portfolio.

**Definition 3:** An elementary portfolio is a portfolio that contains only projects of the same category. It will be expressed in the form of a C-dimensional vector, where C is the number of discrete categories. Each dimension corresponds to one particular category. The value in each dimension corresponds to the number of projects in the associated category. Consequently, the C-dimensional vector of an elementary portfolio with n projects will have the form (0, 0, ..., n, 0, ..., 0).

**Assumption 5:** The SDM can define a complete relation ≽ on the set of elementary portfolios. That is, for any pair of elementary portfolios, P and Q, one and only one of the following propositions is true.
- Portfolio P is preferred to portfolio Q
- Portfolio Q is preferred to portfolio P
- Portfolios P and Q are indifferent.

**Assumption 6 (Essentiality):** Given two elementary portfolios, P and Q, defined over the same category. Let P = (0, 0, ..., n, 0, ..., 0) and Q = (0, 0, ..., m, 0, ..., 0). P is preferred to Q if and only if n > m.

From the set of discrete categories, let C₁ be the lowest category, C_L be the highest, and C_j a category preferred to C₁.

**Assumption 7 (Archimedean):** For any category C_j there is always an integer value n such that the SDM would prefer a portfolio composed of n projects in the C₁ category to any portfolio composed of a single project in the C_j category.

**Assumption 8 (Continuity):** If an elementary portfolio P = (x, 0, ..., 0, ..., 0) is preferred to an elementary portfolio Q = (0, ..., 1, 0, ..., 0), defined over category j for 1 < j ≤ L, there is always a pair of integers values n and m (n > m) such that an elementary portfolio with n projects of the lowest category is indifferent to another elementary portfolio with m projects of the j-th category.

Assumption 5 characterizes the normative claim of the functional approach for decision-making. Assumption 6 is a consequence of Assumption 4 (additivity) combined with the premise that all projects satisfy minimal acceptability requirements. Assumption 7 is a consequence of both essentiality and the non-bounded character of the set of natural numbers. Assumption 8 simulates the way in which a person balances using a scale using a set of two types of weights whose values are relative primes.

Let us say that c₁ is a number representing the subjective value of the projects belonging to the lower category C₁. Similarly, let us use c_j to represent the value of projects in category C_j. Now, suppose that the elementary portfolios P (containing n projects in C_j) and Q (integrated by m projects in C_j) are indifferent. That is, P and Q have the same V value. If we combine Assumption 8 with Equation 2, we obtain the following expression.

function of the set of supported projects. When a non-fuzzy model includes the binary indicator function of a crisp set, the fuzzy generalization provided by classical “fuzzy technology” is made substituting this function with a membership function expressing “the degree of membership” to the more general fuzzy set. In this way, Equation 5 becomes Equation 6 shown below.

U = Σ_ik w_ik μ_ik  (6)

Equation 6 was proposed by Fernandez and Navarro (2002) as a measure of a portfolio’s subjective value.

## 3.3 Synergy and redundancy

Redundancy between projects can be addressed using constraints. For every pair of redundant projects, (p_i, p_j), i < j, condition μ_i(d_i) × μ_j(d_j) = 0 should be enforced.

Let S = {S1, S2, ..., Sk} be the set of coalitions of synergistic projects. In a model like the one represented by Equation 5, each of these coalitions should be treated as an (additional) individual project. As a result, each coalition has an associated cost (i.e., the sum of the costs of the individual projects in the coalition), and an evaluation. This evaluation should be better than the evaluation of any of the projects in the coalition. Let us assume that coalitions S_i and S_j become projects P_N+i and P_N+j, respectively. If S_i is a subset of S_j, then it does not make sense to include them both in a portfolio. Therefore, P_N+i and P_N+j must be considered redundant projects. Furthermore, if project p_k is a member of S_i then the pair (p_k, P_N+i) is also redundant (since the value of p_k is included in the value of P_N+i).

## 3.4 A Genetic algorithm for optimizing public portfolio subjective value

Suppose that a feasible region of portfolios, R_f, is defined by constraints on the total budget and on the distribution of projects by area. In addition, the SDM could include further constraints on the portfolios due to following reasons.
- The particular budget distribution of the portfolio could be very difficult to justify. Let us suppose that the SDM asserts that “project p_i is much better than project p_j”. In consequence, any portfolio in which μ_i is greater than μ_j could be unacceptable. This implies the existence of some veto situations that can be modeled with the following constraint. For every project pair p_i and p_j being s_i and s_j their corresponding evaluations, if (s_i - s_j) ≥ v_s, then (μ_i (d_i) - μ_j (d_j)) must be greater than (or equal to) 0, where v_s is a veto threshold. In the following they will be called veto constraints.
- A possible redundancy exists between projects.

Let us use R'_f, R'_f ⊂ R_f, to denote the set of values for the decision variables that make every portfolio acceptable. All the veto constraints are satisfied in R'_f and there are no redundant projects in the portfolios belonging to this region. The optimization problem can now be defined as follows.

Problem definition 2. An optimal portfolio can be selected by maximizing U = Σ_ik f_i,k (μ_i,k (d_i,k)) w_i,k, subject to d ∈ R'_f, where d_i,k indicates the financial support assigned to the k-th project belonging to the i-th category.

Solving this problem requires a complex non linear programming algorithm. The number of decision variables involved can be in the order of thousands. Due to the discontinuity of μ_i, the objective function is discontinuous on the hyper planes defined by d_k = m_k. Therefore, its continuity domain is not connected. The shape of the feasible region R_f is too convoluted, even more if synergy and redundancy need to be addressed. R_f hardly has the mathematical properties generally required by non linear programming methods. Note that veto constraints on the pairs of projects (p_i, p_k) and (p_k, p_i) are discontinuous on the hyper planes defined by d_k = m_k and d_k^v = m_k^v. In a real world scenario, where hundreds or even thousands of projects are considered, non-linear programming solutions cannot handle these situations. Using Equation 6, a simplified form of Problem definition 2, was efficiently solved by Fernandez et al. (2009) and later by Litvinchev et al. (2010) using an integer-mixed programming model. Unfortunately, this approach cannot handle synergy, redundancy, veto constraints, nor can it handle the non-linear forms of function f in Problem definition 2.

Evolutionary algorithms are less sensitive to the shape of the feasible region, the number of decision variables, and the mathematical properties of the objective function (e.g., continuity, convexity, differentiability, and local extremes). In contrast, all of these issues are a real concern for mathematical non linear programming techniques (Coello, 1999). While evolutionary algorithms are not time-efficient, they often find solutions that closely approximate the optimal. Problem definition 2 represents a relatively rough model. However, the main interest is not on fine tuning the optimization process but rather on the generality of the model and on the ability to reach the optimal solution or a close approximation.

In Figure 1, we illustrate the genetic algorithm used for solving the optimization problem stated in Problem definition 2. This algorithm is based on the work of Fernandez and Navarro (2005). As in any genetic algorithm, a fundamental issue is defining a codification for the set of feasible solutions to the optimization problem. In this case, each individual represents a portfolio and each chromosome contains N genes, where N is the number of projects. For the chromosome, we use a floating point encoding representing the distribution of funding among the set of projects in the portfolio. The financial support for each project is represented by its membership function, μ_i(d_i), which is real-valued with range in [0, 1]. That is, a floating point number represents each project's membership value. This membership value is a gene in our definition of chromosomes. As discussed earlier, the number of genes can be increased in order to address the effects of synergetic projects.

The fitness value of each individual is calculated based on function U given by Equation 5. Remember that this is a subjective value that captures the SDM's certainty that the project receives the necessary funding for its operation. The SDM's idea that a project has been assigned sufficient funds is modeled using two parameters, α and β. The domain for both parameters is the continuous interval [0, 1]. The first parameter, α, can be interpreted as the degree of truth of the assertion "the project has sufficient financial support if it receives m monetary units of funding". When this financial support reaches the value βM, the predicate "the project has sufficient funding" is considered true. The value of these two parameters is needed to establish models for function μ_i in order to calculate the value of U. To generate
