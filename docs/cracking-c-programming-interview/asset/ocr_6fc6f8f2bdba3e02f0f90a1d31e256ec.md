and default (if it's there) will execute until the break is encountered
or the end of the switch.

+   21. c
    - gcc: garbage, garbage
    - turboC: 700, 500
    - **Explanation**: It is a compiler-dependent program.

+   22. d
    - **Explanation**: The *case* label must be a constant or constant
expression. The variable/non-constant expression is not allowed in the
case case label. The enumerated type can also be used as a case
label statement.

+   23. c
    - **Explanation**: As we discussed in the above explanation, the
constant expressions are allowed as a *case* label. Here, the error
is due to duplication in the case case label.

+   24. c
    - **Explanation**: The variable 'i' is visible to the inside block only. But
we can access its value through address out of the block because
the lifetime of the address of a block in a main exists till the exit
of the main function.

+   25. c
    - **Explanation**: The variable 'p' is a constant integer and stored in
t read-only memory area. Its value cannot be updated. In our
program, we are updating the value of 'p' at line 2. Hence,
the compiler will throw an error.

+   26. b
    - **Explanation**: In the gcc compiler, the lexical (phase of
compilation) scanning of symbols starts from left to right. The
operator (++, +, -, ++) which comes first will be treated as the first
symbol. Here, i++j can be treated in two ways, either (i++)+j or i+
(++j). The first operator is '+' which comes in lexical scanning but
after '+', the '+' symbol again encounters and now the first
operator becomes '++'.