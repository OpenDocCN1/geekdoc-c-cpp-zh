```
    Statement:
        Expression
        Print
        Quit

    Print:
        ;

    Quit:
        q

    Expression:
        Term
        Expression + Term
        Expression − Term
    Term:
        Primary
        Term * Primary
        Term / Primary
        Term % Primary
    Primary:
        Number
        ( Expression )
        − Primary
        + Primary
    Number:
        floating-point-literal

    Input comes from cin through the Token_stream called ts.
*/
```

Here we used the block comment, which starts with a `/*` and continues until a `*/`.
In a real program, the revision history would contain indications of what corrections and improvements were made.

Note that the comments are not the code. In fact, this grammar simplifies a bit: compare the rule for **Statement** with what really happens (e.g., have a peek at the code in the following section). The comment fails to explain the loop in `calculate()` that allows us to do several calculations in a single run of the program. We’ll return to that problem in §7.8.1.