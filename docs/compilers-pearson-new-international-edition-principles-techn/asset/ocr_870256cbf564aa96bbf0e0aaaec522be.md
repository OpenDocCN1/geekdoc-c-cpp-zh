# 9.4.  CONSTANT PROPAGATION

# 9.4.1  Data-Flow Values for the Constant-Propagation Framework

The set of data-flow values is a product lattice, with one component for each variable in a program. The lattice for a single variable consists of the following:

+   1. All constants appropriate for the type of the variable.
+   
+   2. The value NAC, which stands for not-a-constant. A variable is mapped to this value if it is determined not to have a constant value. The variable may have been assigned an input value, or derived from a variable that is not a constant, or assigned different constants along different paths that lead to the same program point.
+   
+   3. The value UNDEF, which stands for undefined. A variable is assigned this value if nothing may yet be asserted; presumably, no definition of the variable has been discovered to reach the point in question.

Note that NAC and UNDEF are not the same; they are essentially opposites. NAC says we have seen so many ways a variable could be defined that we know it is not constant; UNDEF says we have seen so little about the variable that we cannot say anything at all.

The semilattice for a typical integer-valued variable is shown in Fig. 9.25. Here the top element is UNDEF, and the bottom element is NAC. That is, the greatest value in the partial order is UNDEF and the least is NAC. The constant values are unordered, but they are all less than UNDEF and greater than NAC. As discussed in Section 9.3.1, the meet of two values is their greatest lower bound. Thus, for all values *v*,

$$\mathrm{UNDEF} \land v = v \quad\text{and}\quad \mathrm{NAC} \land v = \mathrm{NAC}.$$

For any constant *c*,

$$c \land c = c$$

and given two distinct constants *c₁* and *c₂*,

$$c_1 \land c_2 = \mathrm{NAC}.$$

A data-flow value for this framework is a map from each variable in the program to one of the values in the constant semilattice. The value of a variable *v* in a map *m* is denoted by *m(v)*.

# 9.4.2  The Meet for the Constant-Propagation Framework

The semilattice of data-flow values is simply the product of the semilattices like Fig. 9.25, one for each variable. Thus, *m* ≤ *m′* if and only if for all variables *v* we have *m(v)* ≤ *m′(v)*. Put another way, *m* ∧ *m′* = *m″* if *m″(v) = m(v) ∧ m′(v)* for all variables *v*.