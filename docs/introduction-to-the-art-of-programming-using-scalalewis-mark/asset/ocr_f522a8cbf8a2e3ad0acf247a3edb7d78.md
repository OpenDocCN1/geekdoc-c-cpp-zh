# 4.6.2 Summary of Concepts

+   - Constructs that allow different pieces of code to be executed depending on different conditions in the code are called conditionals.
+   - The most basic conditional is if.
+     - The syntax is if(condition) trueExpression else falseExpression.
+     - The condition needs to be an expression with the Boolean type.
+     - In Scala it can be used as an expression with a value or as a statement. As an expression, you need to have an else clause.
+     - Curly braces can define blocks of code that function as a large expression. The value of the expression is the value of the last statement in the block.
+   - The Boolean expressions often involve comparisons of values.
+     - Any values can be checked for equality or inequality using == or !=, respectively.
+     - Values that have a natural ordering can also be compared using <, <=, >, or >=.
+   - More complex Boolean expressions can be built by combining simple expressions using Boolean logic.
+     - The || operator is an inclusive or. This means that it is true if either of the two arguments are true as well as when both are true.
+     - The && operator represents a logical and. It is only true when both arguments are true.
+     - The ^ operator represents exclusive or. This is “or” as used in normal English where the result is true if one argument or the other is true, but not both.
+     - The ! operator is logical negation.
+     - The || and && operators are short-circuit operators.
+   - When building large expressions, the order in which operators are applied is significant. This is called precedence. The precedence of operators in Scala depends on the first character. Table 4.3 gives a full list or precedence in Scala.
+   - Bits can be viewed as Boolean values. Bit-wise arithmetic is operations that work on numeric numbers as collections of bits instead of normal numbers.
+     - | is bit-wise or.
+     - & is bit-wise and.
+     - ^ is bit-wise xor.
+     - ~ is bit-wise negation.

# 4.6.3 Self-Directed Study

Enter the following statements into the REPL and see what they do. Try some variations to make sure you understand what is going on. Note that some lines read values so the REPL will pause until you enter those values. The outcome of other lines will depend on what you enter.