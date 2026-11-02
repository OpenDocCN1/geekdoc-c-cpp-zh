+   - The value of SPARK_Mode cannot be changed over small-scale constructs such as subexpressions of an expression or individual statements in a subprogram. SPARK_Mode can only be changed at the granularity of larger constructs such as subprograms and packages.
+   - It is permitted for code in SPARK to call libraries written in some other language such as C provided the programmer writes a SPARK declaration for each foreign operation. The programmer takes responsibility for ensuring that the library actually conforms to the SPARK aspects declared by the programmer; the SPARK tools cannot check them.
+   - When calling C from SPARK, it is sometimes necessary to write a small helper function that gathers the return value of the underlying C function and returns it as an “out” parameter. This allows you to write the interface to the function as a procedure and work around SPARK’s restriction on functions with out parameters.
+   - Access to information external to the program such as external hardware subsystems is possible by declaring external variables. Commonly, a package is created that wraps the external subsystem with abstract state declared as an external variable.
+   - By default external variables are assumed to have asynchronous readers and writers, meaning that the external subsystem accesses those variables at a time outside the program’s control.
+   - By default external variables are assumed to always have effective reads and writes, meaning that each read of the external variable may produce a new value and that every write is significant, even if the same value is written twice in succession.
+   - External variables with other combinations of asynchronous readers and writers and effective reads and writes can be declared to handle specialized circumstances.
+   - Hierarchical external state abstractions provide a way to simplify complex external states.

# ## Exercises

+   7.1 What are the advantages of allowing parts of a program to not be in SPARK? What are the dangers of doing so?
+   7.2 The Ada compiler defaults to having SPARK_Mode off. Why? When writing a high-integrity program, you would normally want as much of the program to be in SPARK as feasible. How could you arrange for that to happen in a convenient and robust way?