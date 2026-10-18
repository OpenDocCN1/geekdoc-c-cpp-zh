called global variable, its visibility is spread all across the program that means, it is accessible by all the functions present in the program. The lifetime of an external variable is same as the lifetime of a program.

**_Static:_** A static variable has the visibility of a local variable but the lifetime of an external variable. That means, once declared inside a function block, it does not get destroyed after the function is executed, but retains its value so that it can be used by future function calls.

**_Register:_** Similar in behaviour to an automatic variable, a register variable differs in the manner in which it is stored in the memory. Unlike, automatic variables that are stored in the primary memory, the register variables are stored in CPU registers. The objective of storing a variable in registers is to increase its access speed, which eventually makes the program run faster. However, it may be noted that it is not an obligation for a compiler to store a register type variable only in CPU registers, but if there are no registers vacant to accommodate the variable then it is stored just like any other automatic variable.

Table 3.4 gives a summary of the four storage classes:

\begin{tabular}{ccccc}
 & Automatic & External & Static & Register \\
Lifetime & Function block & Entire program & Entire program & Function block \\
Visibility & Local & Global & Local & Local \\
Initial Value & Garbage & 0 & 0 & Garbage \\
Storage & Stack segment & Data segment & Data segment & CPU Registers \\
Purpose & Local variables used by a single function & Global variables used throughout the program & Local variables retaining their values throughout the program & Variables using CPU registers for storage purpose \\
Keyword & auto & extern & static & Register \\
\end{tabular}