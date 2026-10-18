+   10. Write a software mechanism to recursively traverse a directory and all of its subdirectories and perform an action supplied in the form of a functional object passed as a parameter (this can be a composite pattern).

+   11. Refactor the `CC_GUI` class to keep all the positions and dimensions of the controls in a separate resource file (see Listings 6.8 and 6.9). In the class initialization procedure, open that file, read the data, and properly set up the widgets. Do not forget about controlling data correctness.

+   12. Design and implement an extended version of the *CurrencyCalc_GUI* project to allow for currency type conversions in both directions, as well as choosing an arbitrary reference currency.

+   13. Find out how to create a dynamically loaded library in your OS. Remake the static library presented in Section 6.2.6 into a dynamic one, and test its behavior. What are the advantages and disadvantages of both types of libraries?

+   14. Refactor the `SyntaxTree_Test` function defined in Listing 6.27 to accept user-supplied expressions.

+   15. Extend the lexical analysis to allow for white symbols (space, tabs, etc.) and C++ numbers. For this purpose, define and use the grep patterns discussed in Section 6.2.1.

+   16. Derive a new interpreter class that accepts not only numbers but also symbols, so such expressions as `a + 3.14 * b` are recognizable. Then construct a symbol table containing the associations of symbols with their values and write a visitor to evaluate expressions.

+   17. Extend the interpreter to accept function calls with various arguments.

+   18. Design and implement a code-generation visitor for runtime evaluation of any expression. The visitor should generate text, which will be C++ statements. These will form a new program that, after a separate compilation, will provide the final code for evaluating runtime expressions. See “Simple code generation for a stack machine” in (Dick et al. 2012). This idea can be further extended to create your own simple language generator.

+   19. Implement a simple calculator using the Boost Spirit library (Boost.org 2020).

+   20. *Reflection* is a technique that lets us inspect a class without having any information about it. Especially when implementing template functions and classes, for example, we might be interested in verifying whether a type for template instantiation contains certain data or the method for a proper call. Such features will be available soon in the C++ standard. But until then, we can try to implement at least some of this functionality. For example, a reflection method can be added to a class, which returns a `std::tuple` conveying all of its data (Section 3.17). Such a reflection-aware class can be easily compared, streamed out, etc. This technique is shown in the following code, which presents a partial definition of the TBook class:

```
class TBook
{
    std::string    fAuthor;
    std::string    fTitle;
    int            fPubYear {};

```