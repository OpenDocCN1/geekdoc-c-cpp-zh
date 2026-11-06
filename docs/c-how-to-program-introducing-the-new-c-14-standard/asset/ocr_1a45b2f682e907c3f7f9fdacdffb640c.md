*Note the difference between the “seventh element of the `array`” and “`array` element 7.” Subscripts begin at 0, so the “seventh element of the `array`” has the subscript 6, while “`array` element 7” has the subscript 7 and is actually the eighth element of the `array`. This distinction is a frequent source of **off-by-one errors**. To avoid such errors, we refer to specific `array` elements explicitly by their `array` name and subscript number (e.g., `c[6]` or `c[7]`).*

The brackets that enclose a subscript are actually an *operator* that has the same precedence as parentheses used to call a function. **Figure 7.2** shows the precedence and associativity of the operators introduced so far. The operators are shown top to bottom in decreasing order of precedence with their associativity and type.

# **Fig. 7.2 Precedence and associativity of the operators introduced to this point.**

| Operators | Associativity | Type |
|---|---|---|
| `::  ()` | left to right<br><br>*[See caution in Fig. 2.10 regarding grouping parentheses.]* | primary |
| `()  []  ++  --`<br>`static_cast<type>`<br>`(operand)` | left to right | postfix |
| `++  --  +  −  !` | right to left | unary (prefix) |
| `*  /  %` | left to right | multiplicative |