attempt to discharge them regardless of the assertion policy setting. Thus, static verification is unaffected by the `Assertion_Policy` pragma.

# ## Summary

+   - A logical error is an error in the program’s logic as a result of programmer oversight. A runtime error is a special kind of logical error that is detected by Ada-mandated runtime checks.
+   - An assertion is a programmer-defined check. All assertions are executable under the control of the assertion policy in force when a unit is compiled. A policy of Check enables assertions. A policy of Ignore disables them. If an assertion fails during execution, `Assertion_Error` is raised.
+   - The SPARK tools attempt to prove that a program is free of runtime errors and, in addition, all programmer supplied assertions will always be satisfied.
+   - SPARK eliminates `Program_Error` and `Tasking_Error` by prohibiting the features that might raise them.
+   - SPARK does not eliminate the possibility of `Storage_Error`, but it simplifies the analysis required to eliminate it.
+   - SPARK eliminates `Constraint_Error` as part of proving freedom of runtime errors.
+   - At each point where a check is required, either as mandated by the Ada standard or as added by the programmer in the form of an assertion, the SPARK tools generate a verification condition that, if proved, shows the check will never fail.
+   - A precondition is an assertion attached to a subprogram that must hold whenever the subprogram is called. It can be used to constrain the inputs to a subprogram beyond the constraints imposed by the type system. In particular, preconditions can describe required relationships between inputs.
+   - A postcondition is an assertion attached to a subprogram that must hold whenever the subprogram returns. It describes the effect of the subprogram and is part of the subprogram’s functional specification.
+   - In a postcondition, you can use the `'Old` attribute to reference the value of an input when the subprogram is first entered. You can use the `'Result` attribute to reference the return value of a function.
+   - The `Initial_Condition` aspect can be used on a package to specify the state the package has after elaboration. It serves as a kind of package-wide postcondition and is most useful for packages that have internal state.
+   - Assertions in the visible part of a package cannot directly reference information in the private section of a package. It is thus sometimes necessary to define and use public functions in such assertions.