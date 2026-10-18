\begin{tabular}{ccc}
Caption & Meaning & Examples \\
[\&] [\&a] & Capture by reference: 1. Capture all local objects by reference. This opens access to all local objects in the lambda. Capture by reference is potentially risky since a lambda expression can outlive its parameters. In such a case, the lambda may attempt to access a dangling pointer or reference. Thus, a safer way is to create copies of passed objects. 2. Explicitly specify exactly what local objects needs to be accessed (safer). Capture object a by reference. & 12 \\
\end{tabular}