the chosen approach depends on the particular problem. In such situations, it is helpful to try to foresee future use cases and call contexts for a given component and choose the most natural, simple, and versatile solution. Usually, this is obtained in an iterative way, after the first version is refined. The beauty of programming comes from the fact that the same thing can be achieved many different ways, frequently with different consequences. This was also the story behind the *CurrencyExchanger* presented in this section. An alternative approach is left as an exercise.

We have learned about the following while working on the *CurrencyCalc* project:

+   - Creating simple classes with a constructor to initialize data
+   - Creating classes with default special members and virtual destructors for future inheritance
+   - Using a `std::map` container to store `<key,value>` pairs
+   - Using structured bindings when accessing elements of a `std::map`
+   - Input/output:
+     - Overloaded `operator <<` and `operator >>` for data output and input
+     - Stream manipulators
+     - Using wide characters (Unicode) with the `std::wstring`, `std::wcout`, `std::wifstream`, and `std::wofstream` objects
+     - Writing to and reading from a file using elements of the filesystem in the `std::filesystem` namespace
+   - Converting `std::wstring` to double with the `stod` function
+   - Using `std::optional` to express an optionally available object
+   - Working with try-catch statements
+   - Creating software components with defined namespaces
+   - Accessing the system time with objects from `std::chrono::system_clock`

In Section 6.2 we will further extend the *CurrencyCalc* project.

# 3.19 Operators

In the tables in this section, we list all of the C++ operators, ordered by their precedence, with short explanations and brief examples. Remember that not all operators are equally important when writing C++ programs. Also, some of them are rarely used or obsolete. For some, a full description appears in future chapters. For completeness, differences between C- and C++-specific operators are indicated (Appendix A.2).

To fully understand the way the operators work, we need to define an *l-value* and an *r-value*:

+   - *l-value* – An object that can be used on the left side of the assignment operator (`=`). That is, it must be an object that can be assigned to
+   - *r-value* – An object on the right side of the assignment operator. That is, it is an object acting as a value

The next important concepts are operator precedence and associativity:

+   - *Precedence* – When evaluating an expression, a rule indicating which operation should be performed before the others
+   - *Associativity* – A rule for selecting the first operator to execute when there is a choice between operators of the same precedence. Most of the C++ operators are left-associative except for the unary and assignment operators, which are right-associative. An associative rule must be