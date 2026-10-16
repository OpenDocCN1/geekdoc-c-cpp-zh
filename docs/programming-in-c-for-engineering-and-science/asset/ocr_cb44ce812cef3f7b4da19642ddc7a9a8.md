+   - A simple function can be inlined to avoid the overhead of calling that function and thereby reduce execution time. Prepend the keyword `inline` to the function heading to do this.
+   - The signature of a function is the list of its parameter types. A function may overload another function (i.e., have the same name) provided they have different signatures.
+   - Preceding the prototype and the definition of a function with a template clause of the form `template<typename T>` converts the function into a function template, which is a type-independent pattern for a function. When the function is called, the compiler will use the type of the arguments to determine what type to substitute for `T` and generate a type-specific function.

# Style and Design Tips

+   - *Functions should be documented in the same way that programs are. The documentation should include specifications and descriptions of:*
+     - The purpose of the function
+     - Any items that must be received by the function from its caller
+     - Any items that must be input to the function
+     - Any items that are returned or passed back by the function to its caller
+     - Any items that are output by the function
+   - *Follow the same stylistic standards for functions that are used for main programs.*
+   - *Declaring variable objects as close as possible to their first use increases the readability of a program and also aids with debugging.*
+   - *Value parameters receive copies of the corresponding arguments and are used for simple/small arguments. For arguments such as classes (and arrays studied in the next chapter) that are stored in large amounts of memory, use const reference parameters.*
+   - *Use a `return` statement to return a single value from a function; use reference parameters when several values are to be returned.*
+   - *All variables used within a function should be defined within that function, either as parameters or as local variables. This keeps functions self-contained and increases their generality and reusability.*
+   - *Recursive functions should be clearly marked as such. For clarity and readability, the anchor case and inductive steps of a recursive function should be marked with comments.*
+   - *Only simple functions should be specified as being inline functions. Substitution of an inline function's body for each of its calls can increase a program's size considerably if the function is nontrivial and/or it is called at several places in the program.*