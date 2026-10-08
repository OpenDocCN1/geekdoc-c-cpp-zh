# 1.8 Keywords to Frequent

Rules:

+   a. The static keyword shall be used to declare all functions and variables that do not need to be visible outside of the module in which they are declared.

+   b. The const keyword shall be used whenever appropriate. Examples include:
i. To declare variables that should not be changed after initialization,
ii. To define call-by-reference function parameters that should not be modified (e.g., char const * param),
iii. To define fields in a struct or union that should not be modified (e.g., in a struct overlay for memory-mapped I/O peripheral registers), and
iv. As a strongly typed alternative to #define for numerical constants.

+   c. The volatile keyword shall be used whenever appropriate. Examples include:
i. To declare a global variable accessible (by current use or scope) by any interrupt service routine,
ii. To declare a global variable accessible (by current use or scope) by two or more threads,
iii. To declare a pointer to a memory-mapped I/O peripheral register set (e.g., timer_t volatile * const p_timer), and
iv. To declare a delay loop counter.