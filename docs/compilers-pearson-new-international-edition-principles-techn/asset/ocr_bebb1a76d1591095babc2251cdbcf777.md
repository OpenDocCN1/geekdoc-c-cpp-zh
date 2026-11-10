# 9.9. SUMMARY OF CHAPTER 9

block, respectively. The transfer functions for the statements in a block are composed to get the transfer function for the block as a whole.

+   - **Reaching Definitions:** The reaching-definitions data-flow framework has values that are sets of statements in the program that define values for one or more variables. The transfer function for a block kills definitions of variables that are definitely redefined in the block and adds (“generates”) those definitions of variables that occur within the block. The confluence operator is union, since definitions reach a point if they reach any predecessor of that point.

+   - **Live Variables:** Another important data-flow framework computes the variables that are live (will be used before redefinition) at each point. The framework is similar to reaching definitions, except that the transfer function runs backward. A variable is live at the beginning of a block if it is either used before definition in the block or is live at the end of the block and not redefined in the block.

+   - **Available Expressions:** To discover global common subexpressions, we determine the available expressions at each point — expressions that have been computed and neither of the expression’s arguments were redefined after the last computation. The data-flow framework is similar to reaching definitions, but the confluence operator is intersection rather than union.

+   - **Abstraction of Data-Flow Problems:** Common data-flow problems, such as those already mentioned, can be expressed in a common mathematical structure. The values are members of a semilattice, whose meet is the confluence operator. Transfer functions map lattice elements to lattice elements. The set of allowed transfer functions must be closed under composition and include the identity function.

+   - **Monotone Frameworks:** A semilattice has a < relation defined by a < b if and only if a ∧ b = a. Monotone frameworks have the property that each transfer function preserves the ≤ relationship; that is, a ≤ b implies f(a) ≤ f(b), for all lattice elements a and b and transfer function f.

+   - **Distributive Frameworks:** These frameworks satisfy the condition that f(a ∧ b) = f(a) ∧ f(b), for all lattice elements a and b and transfer function f. It can be shown that the distributive condition implies the monotone condition.

+   - **Iterative Solution to Abstract Frameworks:** All monotone data-flow frameworks can be solved by an iterative algorithm, in which the IN and OUT values for each block are initialized appropriately (depending on the framework), and new values for these variables are repeatedly computed by applying the transfer and confluence operations. This solution is always safe (optimizations that it suggests will not change what the