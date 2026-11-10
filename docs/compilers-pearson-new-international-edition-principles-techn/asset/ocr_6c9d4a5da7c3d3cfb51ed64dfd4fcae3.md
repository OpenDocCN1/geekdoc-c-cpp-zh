# ### 7.3.1 Data Access Without Nested Procedures

In the C family of languages, all variables are defined either within a single function or outside any function (“globally”). Most importantly, it is impossible to declare one procedure whose scope is entirely within another procedure. Rather, a global variable *v* has a scope consisting of all the functions that follow the declaration of *v*, except where there is a local definition of the identifier *v*. Variables declared within a function have a scope consisting of that function only, or part of it, if the function has nested blocks, as discussed in Section 1.6.3.

For languages that do not allow nested procedure declarations, allocation of storage for variables and access to those variables is simple:

+   1. Global variables are allocated static storage. The locations of these variables remain fixed and are known at compile time. So to access any variable that is not local to the currently executing procedure, we simply use the statically determined address.
+   2. Any other name must be local to the activation at the top of the stack. We may access these variables through the *top_sp* pointer of the stack.

An important benefit of static allocation for globals is that declared procedures may be passed as parameters or returned as results (in C, a pointer to the function is passed), with no substantial change in the data-access strategy. With the C static-scoping rule, and without nested procedures, any name nonlocal to one procedure is nonlocal to all procedures, regardless of how they are activated. Similarly, if a procedure is returned as a result, then any nonlocal name refers to the storage statically allocated for it.

# ### 7.3.2 Issues With Nested Procedures

Access becomes far more complicated when a language allows procedure declarations to be nested and also uses the normal static scoping rule; that is, a procedure can access variables of the procedures whose declarations surround its own declaration, following the nested scoping rule described for blocks in Section 1.6.3. The reason is that knowing at compile time that the declaration of *p* is immediately nested within *q* does not tell us the relative positions of their activation records at run time. In fact, since either *p* or *q* or both may be recursive, there may be several activation records of *p* and/or *q* on the stack.

Finding the declaration that applies to a nonlocal name *x* in a nested procedure *p* is a static decision; it can be done by an extension of the static-scope rule for blocks. Suppose *x* is declared in the enclosing procedure *q*. Finding the relevant activation of *q* from an activation of *p* is a dynamic decision; it requires additional run-time information about activations. One possible solution to this problem is to use “access links,” which we introduce in Section 7.3.5.