Second, you are not guaranteed smaller and faster binaries. The introduction of complex, explicit error-handling code may soak up all your advantage and yield additional cost. However, if it is important enough, if it is worth the trade-off, engineers will write code to accommodate the absence of exception handling. It’s not a pretty sight, but needs must when the devil drives.

However, if your codebase does permit exception handling, then single return statements carrying the successfully computed value back to the call site become the normal way of things. Multiple return statements might signal a function that is trying to do too much.

# Writing good functions

There are nearly fifty Core Guidelines about functions. We give two of them their own chapter, but it’s worth considering some others here in the context of multiple return statements. For example, Core Guideline F.2: “A function should perform a single logical operation.” Although this guideline talks about splitting larger functions into smaller component functions, and viewing large numbers of parameters with suspicion, one of the side effects of following this advice is that your functions are likely to have a single return instruction, which is the result of the function.

In the same vein, Core Guideline F.3: “Keep functions short and simple.” The function that acts as a counterexample stretches over 27 lines of text and includes three return statements. However, the final example, which puts some of the logic into two helper functions, is nearly a third of the size but still contains three different return instructions, decided upon by the input parameters.

Core Guideline F.8: “Prefer pure functions.” This is a tall order but excellent advice. A pure function is one that does not refer to state outside of its scope. This makes them parallelizable, easy to reason about, more amenable to optimization, and, again, likely to be short and simple.

The important point is that there are very, very few rules that are cast-iron. Rules like that tend to end up being encoded in the language itself. For example, “don’t leak resources” is encoded in the destructor feature and in the library smart pointers. A single return statement might be a sign of