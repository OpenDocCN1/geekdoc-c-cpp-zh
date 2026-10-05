p = nullptr;

indicates that p is pointing nowhere. On most platforms, nullptr maps to address zero, which is out of bounds for running program. Dereferencing p would result in a run-time error, and the problem can be located quickly in a debugger.

C++ allows the literal 0 to be used in place of nullptr.

p = 0;

achieves the same result as assigning nullptr to p. This is how C++ programmers support a pointer to nothing before the nullptr keyword was available. Since newer compilers existing C++ source code, the literal zero assignment works. You should use the nullptr if your compiler supports it because it improves the source readability. Since zero can represent both an integer value and a pointer to integer, both of the following statements are legal if p is declared to be a pointer to integer:

+   * p = 0;
* p = 0;

The first statement assigns null to p, while the second statement sets the data which p points to zero. Another way, the first statement changes what p points; the second statement changes what p points. Superficially, the two statements look very similar and are easy to confuse. Consider the statements below

```
p = nullptr; // OK
p = nullptr; // Error, will not compile
```

The second statement contains an error the nullptr literal may be assigned only to a pointer type.

> The nullptr word is part of the C++11 standard. The name nullptr is simply an identifier (for example, a variable or function name) for older compilers. Before the nullptr constant became available the literal 0 (zero) was considered the nullptr reference. For compatibility with older code, C++11 allows you to use 0 in place of nullptr, but if possible you should avoid this practice when writing new code. The nullptr allows the compiler to perform better type checking. To see why, suppose the programmer believes the variable p is a pointer to an integer, but p is instead a simple integer:
// Programmer believes p is a pointer to an integer
p = 0;
In this case the compiler is powerless to detect a problem because p is an integer, and zero is a valid value. If it really is a pointer then the compiler will flag the following code:
// Programmer believes p is a pointer to an integer
p = nullptr;
because the nullptr may not be assigned to a non-pointer type.

The nullptr constant and the notion of a pointer pointing nowhere becomes more useful when building dynamic data structures (see, for example, Section ??).