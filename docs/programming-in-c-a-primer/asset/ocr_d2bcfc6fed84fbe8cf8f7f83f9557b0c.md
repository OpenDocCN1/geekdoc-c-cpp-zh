# Common Programming Errors

+   - Forgetting to declare an array.
+   - Forgetting to initialize the elements of an array whose elements must be initialized.
+   - Referring an element outside the array bounds (e.g. Off-by-one error).
+   - Referencing the double subscripted array as x [ ] [ ] instead of x [ ].
+   - Referencing a jagged array as x [ ] instead of x[ ] [ ].
+   - Treating an Array type array as an ArrayList type array.
+   - Forgetting to use capital letters for the first characters of the methods and properties used form the namespaces.
+   - Forgetting the use of the System.Collections namespaces while using ArrayList class.

# Review Questions

9.1 State whether the following statements are true or false.

+   (a) It is necessary to specify the size of an array during its declaration.
+   (b) In C#, arrays are created in memory using the operator new.
+   (c) In C#, arrays start with the subscript zero.
+   (d) Trying to access an array beyond its boundaries will cause a run time error.
+   (e) C# arrays are created on the heap.
+   (f) C# arrays cannot store reference type data.
+   (g) A jagged array is declared using the same syntax as that of rectangular arrays.
+   (h) C# permits the assignment of an array object to another.
+   (i) An array of type System.Array is of fixed size.
+   (j) An array of type ArrayList is of fixed size.
+   (k) The default size of an ArrayList array is 16.
+   (l) An array of type ArrayList can contain many different types of objects.
+   (m) An array declaration creates memory space for the array.
+   (n) It is an error if an initializer list contains more values than the number elements in the array.

9.2 Explain the need for array variables.

9.3 What are the two ways to initialize an array of three values?

9.4 Are arrays reference or value types? And where are they created?

9.5 Identify errors, if any, in the following array declaration statements.

+   (a) int score ( );
+   (b) float values [ ];
+   (c) float table [ ] [ ];
+   (d) string name [5];
+   (e) int [ ] m, n;
+   (f) int [d] x;
+   (g) int [ ] counter = int [5];

9.6 Identify errors, if any, in the following initialization statement.

+   (a) int [ ] number = {0, 0, 0};
+   (b) int [ ] x = new int [3] {1, 2, 3, 4};
+   (c) list [3] = {1, 2, 3};
+   (d) int [ ] code = {1, 2, 3,};
+   (e) int [,] table = {0, 0, 0}, {1, 1, 1};
+   (f) float [ ] MARKS = {5.75, 9.25, 6.0};