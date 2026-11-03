+   - Local static variables retain their value between calls to the function in which they're defined.
+   - All numeric variables of static storage duration are initialized to zero if you do not explicitly initialize them.

# Section 5.13 Scope Rules

+   - An identifier's scope (p. 216) is where the identifier can be referenced in a program.
+   - An identifier can have function scope, file scope, block scope or function-prototype scope (p. 216).
+   - Labels are the only identifiers with function scope. Labels can be used anywhere in the function in which they appear but cannot be referenced outside the function body.
+   - An identifier declared outside any function has file scope. Such an identifier is "known" in all functions from the point at which it's declared until the end of the file.
+   - Identifiers defined inside a block have block scope. Block scope ends at the terminating right brace (}) of the block.
+   - Local variables defined at the beginning of a function have block scope, as do function parameters, which are considered local variables by the function.
+   - Any block may contain variable definitions. When blocks are nested, and an identifier in an outer block has the same name as an identifier in an inner block, the identifier in the outer block is "hidden" until the inner block terminates.
+   - The only identifiers with function-prototype scope are those used in the parameter list of a function prototype. Identifiers used in a function prototype can be reused elsewhere in the program without ambiguity.

# Section 5.14 Recursion

+   - A recursive function (p. 219) is a function that calls itself either directly or indirectly.
+   - If a recursive function is called with a base case (p. 219), the function simply returns a result. If it's called with a more complex problem, the function divides the problem into two conceptual pieces: a piece that the function knows how to do and a slightly smaller version of the original problem. Because this new problem looks like the original problem, the function launches a recursive call to work on the smaller problem.
+   - For recursion to terminate, each time the recursive function calls itself with a slightly simpler version of the original problem, the sequence of smaller and smaller problems must converge on the base case. When the function recognizes the base case, the result is returned to the previous function call, and a sequence of returns ensues all the way up the line until the original call of the function eventually returns the final result.
+   - Standard C does not specify the order in which the operands of most operators (including +) are to be evaluated. Of C's many operators, the standard specifies the order of evaluation of the operands of only the operators &&, ||, the comma (,) operator and ?: . The first three of these are binary operators whose two operands are evaluated left to right. The last operator is C's only ternary operator. Its leftmost operand is evaluated first; if it evaluates to nonzero, the middle operand is evaluated next and the last operand is ignored; if the leftmost operand evaluates to zero, the third operand is evaluated next and the middle operand is ignored.

# Section 5.16 Recursion vs. Iteration

+   - Both iteration and recursion are based on a control structure: Iteration uses an iteration statement; recursion uses a selection statement.