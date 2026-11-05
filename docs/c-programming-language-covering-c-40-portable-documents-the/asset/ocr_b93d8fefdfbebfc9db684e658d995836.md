The arguments of properties (§10.7), events (§10.8), and user-defined operators (§10.10) are always passed as value parameters (§10.6.1.1). The arguments of indexers (§10.9) are always passed as value parameters (§10.6.1.1) or parameter arrays (§10.6.1.4). Reference and output parameters are not supported for these categories of function members.

The arguments of an instance constructor, method, indexer, or delegate invocation are specified as an argument-list:

```
argument-list:
    argument
    argument-list , argument

argument:
    argument-name_opt argument-value

argument-name:
    identifier :

argument-value:
    expression
    ref variable-reference
    out variable-reference
```

An argument-list consists of one or more arguments, separated by commas. Each argument consists of an optional argument-name followed by an argument-value. An argument with an argument-name is referred to as a named argument, whereas an argument without an argument-name is a positional argument. It is an error for a positional argument to appear after a named argument in an argument-list.

The argument-value can take one of the following forms:

+   * An expression, indicating that the argument is passed as a value parameter (§10.6.1.1).
+   * The keyword ref followed by a variable-reference (§5.4), indicating that the argument is passed as a reference parameter (§10.6.1.2). A variable must be definitely assigned (§5.3) before it can be passed as a reference parameter.
+   * The keyword out followed by a variable-reference (§5.4), indicating that the argument, is passed as an output parameter (§10.6.1.3). A variable is considered definitely assigned (§5.3) following a function member invocation in which the variable is passed as an output parameter.

# 7.5.1.1 Corresponding Parameters

For each argument in an argument list, there has to be a corresponding parameter in the function member or delegate being invoked.