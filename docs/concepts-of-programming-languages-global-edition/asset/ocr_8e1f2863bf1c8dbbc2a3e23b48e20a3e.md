The mapping function for a given expression E and state s follows. To distinguish between mathematical function definitions and the assignment statements of programming languages, we use the symbol Δ = to define mathematical functions. The implication symbol, =>, used in this definition connects the form of an operand with its associated case (or switch) construct. Dot notation is used to refer to the child nodes of a node. For example, <binary_expr>.<left_expr> refers to the left child node of <binary_expr>.

```
Mₑ (<expr>, s) Δ= case <expr> of
  <dec_num> => M_dec (<dec_num>, s)
  <var> => if VARMAP (<var>, s) == undef
    then error
    else VARMAP (<var>, s)
  <binary_expr> =>
    if (Mₑ (<binary_expr>.<left_expr>, s) == undef OR
        Mₑ (<binary_expr>.<right_expr>, s) == undef)
    then error
    else if (<binary_expr>.<operator> == '+')
      then Mₑ (<binary_expr>.<left_expr>, s) +
           Mₑ (<binary_expr>.<right_expr>, s)
      else Mₑ (<binary_expr>.<left_expr>, s) *
           Mₑ (<binary_expr>.<right_expr>, s)
```

# 3.5.2.4 Assignment Statements

An assignment statement is an expression evaluation plus the setting of the target variable to the expression’s value. In this case, the meaning function maps a state to a state. This function can be described with the following:

```
Mₐ (x = E, s) Δ= if Mₑ (E, s) == error
  then error
  else s' = {<i₁, v₁'>, <i₂, v₂'>, ..., <iₙ, vₙ'>}, where
    for j = 1, 2, ..., n
      if iⱼ == x
        then vⱼ' = Mₑ (E, s)
        else vⱼ' = VARMAP (iⱼ, s)
```

Note that the comparison in the third last line above, iⱼ == x, is of names, not values.

# 3.5.2.5 Logical Pretest Loops

The denotational semantics of a logical pretest loop is deceptively simple. To expedite the discussion, we assume that there are two other existing mapping functions, Mₛₗ and M_b, that map statement lists and states to states and Boolean expressions to Boolean values (or error), respectively. The function is