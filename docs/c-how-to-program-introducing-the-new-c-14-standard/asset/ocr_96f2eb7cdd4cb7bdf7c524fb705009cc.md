# *Section 9.9 `Time` Class Case Study: A Subtle Trap—Returning a Reference or a Pointer to a `private` Data Member*

+   - A reference to an object is an alias for the name of the object and, hence, may be used on the left side of an assignment statement. In this context, the reference makes a perfectly acceptable *lvalue* that can receive a value.
+   - If the function returns a reference to `const` data, then the reference cannot be used as a modifiable *lvalue*.