![](bbox=[0.26, 0.11, 0.74, 0.39])

The reference program

I have two questions in mind for my process of ongoing optimization.

+   1. Is the program well-defined? In particular: is there a data-race?
+   2. Which values for x and y are possible?

The first question is often very challenging to answer. In the first step, I think about the answer to the first question, and in the second step, I verify my reasoning with CppMem. Once I have answered the first question, the second answer can easily be determined from the first answer. I also present the possible values for x and y in a table.

However, I haven't explained what I mean by ongoing optimization. It's pretty simple; I successively optimize the program by weakening the C++ memory-ordering. These are my optimization steps:

+   - Non-atomic variables
+   - Locks
+   - Atomics with sequential consistency
+   - Atomics with acquire-release semantic
+   - Atomics with relaxed semantic
+   - Volatile variables

Before I start my process of ongoing optimization, you should have a basic understanding of CppMem. The chapter CppMem gives you a simplified introduction.