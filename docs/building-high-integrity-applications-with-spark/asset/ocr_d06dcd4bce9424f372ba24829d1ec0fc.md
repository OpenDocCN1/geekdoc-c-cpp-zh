# # 6 Proof

In this chapter we describe how you can use SPARK to prove certain correctness properties of your programs. When you ask to “prove” your code, the SPARK tools will by default endeavor to prove that it will never raise any of the predefined language exceptions that we describe in Section 6.1. If you additionally include pre- and postconditions, loop invariants, or other kinds of assertions, the tools will also attempt to prove that those assertions will never fail.

It is important to understand that proofs created by the SPARK tools are entirely static. This means that if they succeed, the thing being proved will be true for every possible execution of your program regardless of the inputs provided. This is the critical property of proof that sets it apart from testing.

However, Ada assertions are also executable under the control of the assertion policy in force at the time a unit is compiled. Assertions for which proofs could not be completed can be checked when the program is run, for example during testing, to help provide a certain level of confidence about the unproved assertions. Testing can thus be used to complement the proof techniques described here to obtain greater overall reliability. We discuss this further in Section 8.4.

# ## 6.1 Runtime Errors

A logical error is an error in the logic of the program itself that may cause the program to fail as it is executing. It is an error that, in principle, arises entirely because of programmer oversight. In contrast, an external error is an error caused by a problem in the execution environment of the program, such as being unable to open a file because it does not exist. If a program is correct, it should not contain any logical errors. However, external errors are outside of a program’s control and may occur regardless of how well constructed the