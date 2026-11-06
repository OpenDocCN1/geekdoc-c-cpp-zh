easier to debug and modify, and more likely to be bug free in the first place.

+   1. C. Bohm and G. Jacopini, “Flow Diagrams, Turing Machines, and Languages with Only Two Formation Rules,” *Communications of the ACM*, Vol. 9, No. 5, May 1966, pp. 336–371.

Bohm and Jacopini’s work demonstrated that all programs could be written in terms of only three control structures—the **sequence structure**, the **selection structure** and the **iteration structure**. We’ll discuss how each of these is implemented in C++.

# 4.4.1 Sequence Structure

The sequence structure is built into C++. Unless directed otherwise, the computer executes C++ statements one after the other in the order in which they’re written—that is, in sequence. The UML **activity diagram** in [Fig. 4.2](#) illustrates a typical sequence structure in which two calculations are performed in order. C++ lets you have as many actions as you want in a sequence structure. As we’ll soon see, anywhere a single action may be placed, we may place several actions in sequence.