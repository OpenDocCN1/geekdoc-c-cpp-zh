The Option 1 approach can’t be applied consistently in mixed-language environments if any of the languages are case-insensitive. In Microsoft Visual Basic, for example, `Dim widget As Widget` will generate a syntax error because *widget* and *Widget* are treated as the same token.

Option 2 creates a more obvious distinction between the type name and the variable name. For historical reasons, all caps are used to indicate constants in C++ and Java, however, and the approach is subject to the same problems in mixed-language environments that Option 1 is subject to.

Option 3 works adequately in all languages, but some programmers dislike the idea of prefixes for aesthetic reasons.

Option 4 is sometimes used as an alternative to Option 3, but it has the drawback of altering the name of every instance of a class instead of just the one class name.

Option 5 requires more thought on a variable-by-variable basis. In most instances, being forced to think of a specific name for a variable results in more readable code. But sometimes a *widget* truly is just a generic *widget*, and in those instances you’ll find yourself coming up with less-than-obvious names, like *genericWidget*, which are arguably less readable.

In short, each of the available options involves tradeoffs. The code in this book uses Option 5 because it’s the most understandable in situations in which the person reading the code isn’t necessarily familiar with a less intuitive naming convention.

**Identify global variables**  One common programming problem is misuse of global variables. If you give all global variable names a `g_` prefix, for example, a programmer seeing the variable `g_RunningTotal` will know it’s a global variable and treat it as such.

**Identify member variables**  Identify a class’s member data. Make it clear that the variable isn’t a local variable and that it isn’t a global variable either. For example, you can identify class member variables with an `m_` prefix to indicate that it is member data.

**Identify type definitions**  Naming conventions for types serve two purposes: they explicitly identify a name as a type name, and they avoid naming clashes with variables. To meet those considerations, a prefix or suffix is a good approach. In C++, the customary approach is to use all uppercase letters for a type name—for example, `COLOR` and `MENU`. (This convention applies to *typedefs* and *structs*, not class names.) But this creates the possibility of confusion with named preprocessor constants. To avoid confusion, you can prefix the type names with `t_`, such as `t_Color` and `t_Menu`.

**Identify named constants**  Named constants need to be identified so that you can tell whether you’re assigning a variable a value from another variable (whose value might change) or from a named constant. In Visual Basic, you have the additional possibility that the value might be from a function. Visual Basic doesn’t require function names to use parentheses, whereas in C++ even a function with no parameters uses parentheses.