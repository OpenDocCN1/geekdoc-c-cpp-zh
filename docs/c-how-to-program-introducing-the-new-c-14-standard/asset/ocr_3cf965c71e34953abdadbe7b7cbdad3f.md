# Section 9.11 `const` Objects and `const` Member Functions

+   - The keyword `const` can be used to specify that an object is not modifiable and that any attempt to modify the object should result in a compilation error.
+   - C++ compilers disallow non-`const` member function calls on `const` objects.
+   - An attempt by a `const` member function to modify an object of its class is a compilation error.
+   - A member function is specified as `const` both in its prototype and in its definition.
+   - A `const` object must be initialized.
+   - Constructors and destructors cannot be declared `const`.