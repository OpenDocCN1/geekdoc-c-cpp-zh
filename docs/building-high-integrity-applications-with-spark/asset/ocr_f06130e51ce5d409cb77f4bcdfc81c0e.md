+   2. It does mean an ineffective value computed by the caller might appear effective if it participates as an input in a flow dependency that does not actually exist.
+   3. See the *SPARK 2014 Toolset User’s Guide* (SPARK Team, 2014b).

# 5 Mathematical Background

+   1. Arguments in this context are usually called *conjectures* (potential theorems).
+   2. The operator ∈ is for set membership. The expression *x* ∈ *U* is read “*x* is a member of the set of all humans alive today.”

# 6 Proof

+   1. For an explanation of Ada’s exceptions and exception handlers, see Dale and McCormick (2007) or Barnes (2014).
+   2. Examination of the subprogram may also fail if it is not sufficiently implemented to honor its data and flow dependency contracts.
+   3. The older SPARK 2005 does have some support for tasking.
+   4. The assume assertion is special. See Section 6.3.
+   5. The *N*-th Fibonacci number, *F(N)*, is given by *F(N − 1) + F(N − 2)*, where *F(0) = 0* and *F(1) = 1* are base cases.
+   6. In this example, the procedure only searches arrays of exactly 100 integers. In Section 6.7 we show a generic version of this procedure that is more general.
+   7. Recall that limited types cannot be copied.
+   8. *Inline expansion* is a process in which the compiler replaces subprogram calls with copies of the subprogram. This substitution typically improves the execution time and stack memory usage; however, it also increases the size of the program. The aspect Inline is used to request this expansion.
+   9. At the time of this writing SPARK does not support type invariants. However, support is planned for a future version of SPARK.
+   10. At the time of this writing SPARK does not support dynamic predicates. However, support is planned for a future version of SPARK.
+   11. For example, 192.168.56.2.
+   12. The algorithm can be supplemented to deal with single digit divisors (Knuth, 1998), but we do not do so here.
+   13. Secure hash algorithms are used with, for example, digital signature algorithms to provide strong data integrity checks.

# 7 Interfacing with SPARK

+   1. *Library level* means that the program unit is not nested within another program unit. It may be compiled separately and referenced in with and use clauses.
+   2. For an explanation of Ada’s pointers, see Dale and McCormick (2007) or Barnes (2014).
+   3. For an explanation of Ada’s exceptions and exception handlers, see Dale and McCormick (2007) or Barnes (2014).
+   4. For an explanation of Ada’s automatic finalization, see Dale and McCormick (2007) or Barnes (2014).
+   5. For a full treatment of using Ada to interact with hardware, see McCormick, Singhoff, and Hugues (2011).