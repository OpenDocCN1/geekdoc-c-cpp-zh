to reduce the dependency of real number operations on the hardware (and encourages hardware manufacturers to ensure that their processors comply with the standard). C++, Ada, and Java all rely on some form of this standard to make floating-point operations more machine-independent. Indeed, in an attempt to reduce machine dependencies to a minimum, the designers of Java and Ada built into their standards strong requirements for all arithmetic operations. C++, too, has certain minimal requirements as part of its standard, but it is less strict than Ada and Java.

An even more significant issue regarding data types is the disagreement among language designers on the extent to which type information should be made explicit in a programming language and be used to verify program correctness prior to execution. Typically, the line of demarcation is clearest between those who emphasize maximal flexibility in the use of data types and who advocate no explicit typing or translation-time type verification, and those who emphasize maximum restrictiveness and call for strict implementation of translation-time type checking. A good example of a language with no explicit types or translation-time typing is Scheme, while Ada is a good example of a very strictly type-checked language (sometimes referred to as a **strongly typed** language). There are many reasons to have some form of static (i.e., translation-time) type checking, however:

+   1. Static type information allows compilers to allocate memory efficiently and generate machine code that efficiently manipulates data, so **execution efficiency** is enhanced.
+   
+   2. Static types can be used by a compiler to reduce the amount of code that needs to be compiled (particularly in a recompilation), thus improving **translation efficiency**.
+   
+   3. Static type checking allows many standard programming errors to be caught early, improving **writability**, or efficiency of program coding.
+   
+   4. Static type checking improves the **security and reliability** of a program by reducing the number of execution errors that can occur.
+   
+   5. Explicit types in a programming language enhance **readability** by documenting data design, allowing programmers to understand the role of each data structure in a program, and what can and cannot be done with data items.
+   
+   6. Explicit types can be used to **remove ambiguities** in programs. A prime example of this was discussed in the previous chapter (Section 7.4): Type information can be used to resolve overloading.
+   
+   7. Explicit types combined with static type checking can be used by programmers as a **design tool**, so that incorrect design decisions show up as translation-time errors.
+   
+   8. Finally, static typing of interfaces in large programs enhances the development of large programs by verifying **interface consistency and correctness**.

> ²To say that Scheme has no explicit types and no translation-time type checking is not to say that Scheme has no types. Indeed, every data value in Scheme has a type, and extensive checking is performed on the type of each value during execution.