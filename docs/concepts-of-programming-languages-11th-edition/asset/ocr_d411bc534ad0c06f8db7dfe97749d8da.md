subprogram names can be passed as parameters and the language allows subprograms to be nested, there is the question of the correct referencing environment of a subprogram that has been passed as a parameter.

As seen in Chapter 5, side effects of functions can cause problems. So, restrictions on side effects are a design issue for functions. The types and number of values that can be returned from functions are other design issues.

Finally, there are the questions of whether subprograms can be overloaded or generic. An **overloaded subprogram** is one that has the same name as another subprogram in the same referencing environment. A **generic subprogram** is one whose computation can be done on data of different types in different calls. A **closure** is a nested subprogram and its referencing environment, which together allow the subprogram to be called from anywhere in a program.

The following is a summary of these design issues for subprograms in general. Additional issues that are specifically associated with functions are discussed in Section 9.10.

+   * Are local variables statically or dynamically allocated?
+   * Can subprogram definitions appear in other subprogram definitions?
+   * What parameter-passing method or methods are used?
+   * Are the types of the actual parameters checked against the types of the formal parameters?
+   * If subprograms can be passed as parameters and subprograms can be nested, what is the referencing environment of a passed subprogram?
+   * Are functional side effects allowed?
+   * What types of values can be returned from functions?
+   * How many values can be returned from functions?
+   * Can subprograms be overloaded?
+   * Can subprograms be generic?
+   * If the language allows nested subprograms, are closures supported?

These issues and example designs are discussed in the following sections.

# # 9.4 Local Referencing Environments

This section discusses the issues related to variables that are defined within subprograms. The issue of nested subprogram definitions is also briefly covered.

# ## 9.4.1 Local Variables

Subprograms can define their own variables, thereby defining local referencing environments. Variables that are defined inside subprograms are called **local variables**, because their scope is usually the body of the subprogram in which they are defined.