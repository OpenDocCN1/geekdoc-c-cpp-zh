this description information is also printed. Even library procedures, whose body is generally elided when printing, have their description (if any) printed. The descriptionSequence is also used when information about the procedure is printed by the Describe command.

+   - The optional uses usesSequence; clause is equivalent to wrapping the statementSequence with a use statement. In other words, `proc ... uses LinearAlgebra; ... end proc` is equivalent to: `proc ... use LinearAlgebra in ... end use; end proc`
+   - The statementSequence consists of one or more Maple language statements, separated by semicolons (;), implementing the algorithm of the procedure.
+   - A procedure assigned to a name, f, is invoked by using f(argumentSeq). See Argument Processing for an explanation of argument passing.
+   - The value of a procedure invocation is the value of the last statement executed, or the value specified in a return statement.
+   - In both 1-D and 2-D math notation, statements entered between proc and end proc must be terminated with a colon (:) or semicolon (;).

# Implicit Local Variables

+   - For any variable used within a procedure without being explicitly mentioned in a local localSequence; or global globalSequence; the following rules are used to determine whether it is local or global:
+   
+     *The variable is searched for amongst the locals and globals (explicit or implicit) in surrounding procedures, starting with the innermost. If the name is encountered as a parameter, local variable, or global variable of such a surrounding procedure, that is what it refers to. Otherwise, any variable to which an assignment is made, or which appears as the controlling variable in a ‘for’ loop, is automatically made local. Any remaining variables are considered to be global.*
+   
+   - **Note.** Any name beginning with __Env is considered to be an environment variable, and is not subject to the rules above.

# The Operands of a Procedure

+   - A Maple procedure is a valid expression like any other (e.g., integers, sums, inequalities, lists, etc.). As such, it has sub-parts that can be extracted using the op function. A procedure has eight such operands:
+   
+     `op 1` is the parameterSequence,
+   
+     `op 2` is the localSequence,
+   
+     `op 3` is the optionSequence,