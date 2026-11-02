![](bbox=[0.2, 0.115, 0.77, 0.365])

Figure 8.3. Verifying preconditions and postconditions when combining proof and testing.

SPARK’s contracts provides an ideal mechanism for combining proof with testing in such a divided program. How we verify the contracts depends on the relationship between the subprograms in our application:

+   - When a proven subprogram calls another proven subprogram, the preconditions and postconditions of the called subprogram are verified by proof.
+   - When a tested subprogram calls another tested subprogram, the preconditions and postconditions of the called subprogram need to be verified by test.
+   - When a tested subprogram calls a proven subprogram, the preconditions of the proven subprogram need to be verified by test and the postconditions of the proven subprogram are verified by proof (see Figure 8.3a). Calls from different tested subprograms to the same proven subprogram must have the proven subprogram’s preconditions tested separately.
+   - When a proven subprogram calls a tested subprogram, the preconditions of the tested subprogram are verified by proof and the postconditions of the tested subprogram need to be verified by test (see Figure 8.3b).

The 80/20 ratio so common in software engineering seems to fit the model of combined proof and testing. About 80 percent of the subprograms in a typical high integrity program can be “easily” proven, and 80 percent of the remaining subprograms can be “easily” tested. That leaves 4 percent of the subprograms in the difficult-to-verify category.

By setting a switch in our Ada 2012 compiler, the preconditions and postconditions we have written in our subprograms will be checked at runtime.