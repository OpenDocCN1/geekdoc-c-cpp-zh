# ## 6.2 Program Components in C++

As you’ve seen, C++ programs are typically written by combining new functions and classes—you write with “prepackaged” functions and classes available in the C++ Standard Library. The C++ Standard Library provides a rich collection of functions for common mathematical calculations, string manipulations, character manipulations, input/output, error checking and many other useful operations.

Functions allow you to modularize a program by separating its tasks into self-contained units. You’ve used a combination of library functions and your own functions in every program you’ve written. Functions you write are referred to as **user-defined functions** or **programmer-defined functions**. The statements in function bodies are written only once, are reused from perhaps several locations in a program and are hidden from other functions.

There are several motivations for modularizing a program with functions. One is the divide-and-conquer approach. Another is software reuse. For example, in earlier programs, we did not have to define how to read a line of text from the keyboard—C++ provides this capability via the `getline` function of the `<string>` header. A third motivation is to avoid repeating code. Also, dividing a program into meaningful functions makes the program easier to debug and maintain.

> **Software Engineering Observation 6.1**
> 
> *To promote software reusability, every function should be limited to performing a single, well-defined task, and the name of the function should express that task effectively.*

As you know, a function is invoked by a function call, and when the called function completes its task, it either returns a result or simply returns control to the caller. An analogy to this program structure is the hierarchical form of management (Figure 6.1). A boss (similar to the calling function) asks a worker (similar to the called function) to perform a task and report back (i.e., return) the results after completing the task. The boss function does *not* know how the worker function performs its designated tasks. The worker may also call other worker functions, unbeknownst to the boss. This *hiding of implementation details* promotes good software engineering. Figure 6.1 shows the boss function communicating with several worker functions. The boss function divides the responsibilities among the worker functions, and worker1 acts as a “boss function” to worker4 and worker5.

![](bbox=[0.143, 0.727, 0.857, 0.923])

**Fig. 6.1** | Hierarchical boss function/worker function relationship.