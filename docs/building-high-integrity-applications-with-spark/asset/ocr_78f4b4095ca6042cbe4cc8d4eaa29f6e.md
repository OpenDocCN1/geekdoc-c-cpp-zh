# ### 1.3 Spark Tools

Spark comes with a set of tools for developing Spark programs. A full description of the tools is available in the *SPARK 2014 Toolset User’s Guide* (Spark Team, 2014b). In this section we list and provide a very brief summary of these tools. More detailed descriptions of each tool are given in later chapters when appropriate.

# ### 1.3.1 GNAT Compiler

The GNAT compiler performs the tasks of a typical compiler:

+   - Checks that the program is in conformance with all of the Ada syntax and semantic rules.
+   - Generates the executable code.

The *SPARK 2014 Toolset User’s Guide* (Spark Team, 2014b) recommends that our first step in developing a SPARK program is to use the GNAT compiler *semantic check* tool to ensure that the code is valid Ada. Once we have completed the formal verification of our SPARK program, our final step is to use the GNAT compiler to generate the executable code.

For testing purposes, we can request that the compiler generate machine code to check any assertions (preconditions, postconditions, etc.) while the program is running. Should any assertion be found false, the exception Assertion_Error is raised. This capability allows us to perform tests of our assertions prior to proving them.

# ### 1.3.2 GNATprove

GNATprove is the verification tool for SPARK. It may be run in three different modes:

**Check:** Checks that a program unit contains only the subset of Ada that is defined for SPARK.

**Flow:** Performs a flow analysis of SPARK code. This analysis consists of two parts: a *data-flow analysis* that considers the initialization of variables and the data dependencies of subprograms and an *information-flow analysis* that considers the dependencies or couplings between the values being passed into and out of a subprogram.

**Proof:** Performs a formal verification of the SPARK code. Formal verification will point out any code that might raise a runtime error such as division by zero, assignment to a variable that is out of range of the type of the variable, incorrect indexing of arrays, or overflow of an arithmetic