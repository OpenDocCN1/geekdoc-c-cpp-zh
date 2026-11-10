# 9.2. INTRODUCTION TO DATA-FLOW ANALYSIS

+   2. Suppose, instead, we are interested in implementing constant folding. If a use of the variable $x$ is reached by only one definition, and that definition assigns a constant to $x$, then we can simply replace $x$ by the constant. If, on the other hand, several definitions of $x$ may reach a single program point, then we cannot perform constant folding on $x$. Thus, for constant folding we wish to find those definitions that are the unique definition of their variable to reach a given program point, no matter which execution path is taken. For point (5) of Fig. 9.12, there is no definition that must be the definition of $a$ at that point, so this set is empty for $a$ at point (5). Even if a variable has a unique definition at a point, that definition must assign a constant to the variable. Thus, we may simply describe certain variables as “not a constant,” instead of collecting all their possible values or all their possible definitions.

Thus, we see that the same information may be summarized differently, depending on the purpose of the analysis. □

# 9.2.2  The Data-Flow Analysis Schema

In each application of data-flow analysis, we associate with every program point a *data-flow value* that represents an abstraction of the set of all possible program states that can be observed for that point. The set of possible data-flow values is the *domain* for this application. For example, the domain of data-flow values for reaching definitions is the set of all subsets of definitions in the program. A particular data-flow value is a set of definitions, and we want to associate with each point in the program the exact set of definitions that can reach that point. As discussed above, the choice of abstraction depends on the goal of the analysis; to be efficient, we only keep track of information that is relevant.

We denote the data-flow values before and after each statement $s$ by IN[$s$] and OUT[$s$], respectively. The *data-flow problem* is to find a solution to a set of constraints on the IN[$s$]'s and OUT[$s$]'s, for all statements $s$. There are two sets of constraints: those based on the semantics of the statements (“transfer functions”) and those based on the flow of control.

# Transfer Functions

The data-flow values before and after a statement are constrained by the semantics of the statement. For example, suppose our data-flow analysis involves determining the constant value of variables at points. If variable $a$ has value $v$ before executing statement $b = a$, then both $a$ and $b$ will have the value $v$ after the statement. This relationship between the data-flow values before and after the assignment statement is known as a transfer function.

Transfer functions come in two flavors: information may propagate forward along execution paths, or it may flow backwards up the execution paths. In a forward-flow problem, the transfer function of a statement $s$, which we shall