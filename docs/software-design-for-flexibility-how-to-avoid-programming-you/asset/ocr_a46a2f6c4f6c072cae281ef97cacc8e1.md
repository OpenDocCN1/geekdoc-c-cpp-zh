In examples we show the value that would be printed by the Scheme system using *slanted* characters following the input expression.

The logician Alonzo Church [16] invented $\lambda$ notation to allow the specification of an anonymous function of a named parameter: $\lambda$[expression in x]. This is read, “That of one argument whose value is obtained by substituting the argument for x in the indicated expression."

We say that the formal parameters are *bound* to the arguments, and the *scope* of the binding is the body of the procedure.

The examples are indented to help with readability. Scheme does not care about extra white space, so we may add as much as we please to make things easier to read.

A *predicate* is a procedure that returns true or false. By Scheme cultural convention, we usually give a predicate name ending with a question mark (?), except for the elementary arithmetic comparison predicates: =, <, <=, and >=. This is just a stylistic convention. To Scheme the question mark is just an ordinary character.

It is convenient, but irritating to some, the conditional expressions (*if* and *cond*) treat any predicate value that is not explicitly #f as true.

These names are accidents of history. They stand for “Contents of the Address part of Register” and “Contents of the Decrement part of Register” of the IBM 704 computer, which was used for the first implementation of Lisp in the late 1950s. Scheme is a dialect of Lisp.

A symbol may have any number of characters. A symbol may not normally contain whitespace or delimiter, such as parentheses, brackets, quotation marks, comma, and #; but there are special notations that allow any characters to be included in a symbol's name.