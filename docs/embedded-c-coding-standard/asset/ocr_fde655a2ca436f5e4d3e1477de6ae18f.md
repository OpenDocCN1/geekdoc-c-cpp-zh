3. For better or worse (well, mostly worse), the ISO C Programming Language “Standard” permits a considerable amount of variation between compilers. The ISO C Standard’s “implementation-defined,” “unspecified,” and “undefined” behaviors, along with “locale-specific options,” mean that even programs compiled from identical source code but via different “ISO C”-compliant compilers may behave very differently at run-time. Such gray areas in the C language standard greatly reduce the portability of source code that is not carefully crafted.

4. The reliability, readability, efficiency, and sometimes portability of source code is more important than programmer convenience.

5. There are many sources of defects in software programs. The original team of programmers will create some defects. Programmers who later maintain, extend, port, and/or reusing the source code may create additional defects—including as a result of misunderstandings of the original code.

+   * The number and severity of defects introduced by the original programmer(s) can be reduced through disciplined conformance with certain coding practices, such as the placement of constants to the left side of an equivalence (==) test.

+   * The number and severity of defects introduced by maintenance programmers can also be reduced by the original programmer. For example, appropriate use of portable fixed-width integer types (e.g., int32_t) ensures that no future port of the code will encounter an unexpected overflow.

+   * The number and severity of defects introduced by maintenance programmers can also be reduced through the disciplined use of consistent commenting and stylistic practices, so that everyone in an organization can easily understand the meaning and proper use of variables, functions, and modules.

> See, e.g., [C90] and [C99].