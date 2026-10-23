# Solution Search in Static CSPs

There is plenty of literature on algorithms that can be used for solving static constraint satisfaction problems (e.g., Mackworth, 1977; Rossi et al., 2006; Russel and Norvig, 2003; Tsang, 1993). The basic approach of CSP algorithms is to apply backtracking in combination with a couple of additional mechanisms that altogether focus on variable domain size reduction during search (Russel and Norvig, 2003). One basic principle for reducing the domain size of variables is node-consistency, which requires that those values of a variable domain that are inconsistent with an unary constraint are eliminated as options (for these options there does not exist a solution). Arc-consistency (AC) is a property that must be fulfilled by combinations of variables v1 and v2 that are connected via a binary constraint cb9: each value in the domain of v1 must have at least one corresponding value in the domain of v2 such that cb is fulfilled. Note that arc-consistency is directed; if variable v1 is arc-consistent with variable v2 this does not necessarily mean that v2 is arc-consistent with v1. In the following example we take a look at the variables WA and NT of our map configuration (coloring) example (see Figure 6.2). Although AC is restricted to binary constraints, this does not restrict its applicability since every n-ary constraint can be transformed into a corresponding set of binary constraints (e.g., Bacchus and vanBeek, 1998).

Example of node-consistency and arc-consistency. The original domain of WA = {r,g,b}. Since we defined {WA = r} as a requirement, WA is node-consistent and the values {g,b} get removed from its domain. In order to ensure arc-consistency between WA and NT, the value {r} needs to be removed from NT’s domain definition. Now, each value in the new domain of WA has a consistent corresponding value in the domain of NT and vice versa.

Another important principle in variable domain size reduction is forward checking: Depending on the value selected for the current variable, the values of the instantiated variables that can’t be a support for the selected value are eliminated from their corresponding domains. An example is depicted in Figure 6.4.

Search algorithms for CSPs are able to support optimization, which helps to minimize (e.g., the overall price of a configuration) or maximize (e.g., the failure safety of an equipment) solution parameters (Pitiot et al., 2013).

![](bbox=[0.3, 0.66, 0.75, 0.78])

# FIGURE 6.4

A simple example of forward checking. The variables WA and NT already have assigned values (r and g). The only possible remaining value for SA is b; r and g do not have to be checked for consistency with the settings of WA and NT.

9 A constraint that refers to exactly two variables.